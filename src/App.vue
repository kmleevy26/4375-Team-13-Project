<template>
  <div id="app">
    <!-- Title Container -->
    <div class="title-container">
      <h1 class="page-title">UH IT Device Reservations</h1>
    </div>
    <!-- Vertical Navigation Section -->
    <div class="vertical-nav">
      <img src="./assets/UHLOGO.jpg" alt="Logo" class="logo">
      <button @click="navigate('view_inventory')">View Inventory</button>
      <button @click="navigate('view_tickets')">View Support Tickets</button>
      <button @click="navigate('send_ticket')">Send Support Ticket</button>
      <button @click="navigate('logout')">Logout</button>
    </div>

    <!-- Main Area of Page -->
    <div class="main-content">
      <!-- Two Main Buttons -->
      <div class="large-buttons">
        <button @click="navigate('make_reservation')">Make a Reservation <img src="./assets/clipboard_icon.png" alt="Make Reservations Icon" class="icon"></button>
        <button @click="navigate('view_reservations')">View Reservations <img src="./assets/computer_icon.png" alt="View Reservations Icon" class="icon"></button>
      </div>

      <!-- Additional Content Sections -->
      <div v-if="currentSection === 'view_inventory'">
        <!-- Template for view_inventory -->
        <h2 style="color: black;">View Inventory</h2>
        <div>
          <label for="sortSelect">Sort by:</label>
          <select id="sortSelect" v-model="sortOption">
            <option value="name">Name</option>
            <option value="availability">Availability</option>
          </select>
        </div>
        <table class="inventory-table">
          <thead>
            <tr>
              <th @click="sortBy('id')">Student ID</th>
              <th @click="sortBy('name')">Name</th>
              <th @click="sortBy('serialNumber')">Serial Number</th>
              <th @click="sortBy('availability')">Availability</th>
            </tr>
          </thead>
          <tbody>
            <tr v-for="(item, index) in sortedInventory" :key="index">
              <td>{{ item.id }}</td>
              <td>{{ item.name }}</td>
              <td>{{ item.serialNumber }}</td>
              <td>{{ item.available ? 'Available' : 'Unavailable' }}</td>
            </tr>
          </tbody>
        </table>
  </div>

      <div v-if="currentSection === 'view_tickets'">
        <h2>View Support Tickets</h2>
        <!-- Add content related to viewing support tickets -->
      </div>

      <div v-if="currentSection === 'send_ticket'">
        <h2>Send Support Ticket</h2>
        <!-- Add content related to sending support ticket -->
      </div>

      <div v-if="currentSection === 'logout'">
        <!-- Implement logic to logout user -->
      </div>

      <div v-if="currentSection === 'make_reservation'">
        <h2>Make a Reservation</h2>
        <!-- Add content/form to make a reservation -->
      </div>

      <div v-if="currentSection === 'view_reservations'">
        <h2>View Reservations</h2>
        <!-- Add content related to viewing reservations -->
      </div>
    </div>
  </div>
</template>

<!-- Starting Script for inventory -->
<script>
export default {
  data() {
    return {
      currentSection: 'make_reservation',
      inventory: [
        { id: '123', name: 'Laptop', serialNumber: 'ABC123', available: true },
        { id: '124',name: 'Locker', serialNumber: 'DEF456', available: false },
        { id: '126',name: 'Locker', serialNumber: 'GHI789', available: true },
      ],
      sortOption: 'name'
    }
  },
  computed: {
    sortedInventory() {
      return this.inventory.slice().sort((a, b) => {
        if (this.sortOption === 'name') {
          return a.name.localeCompare(b.name);
        } else if (this.sortOption === 'serialNumber') {
          return a.serialNumber.localeCompare(b.serialNumber);
        } else if (this.sortOption === 'availability') {
          return a.available - b.available;
        }
      });
    }
  },
  methods: {
    navigate(section) {
      this.currentSection = section;
    },
    sortBy(option) {
      this.sortOption = option;
    }
  },
};
// Ending Script for inventory
</script>

<style scoped>
body {
  margin: 0;
  padding: 0;
  font-family: Arial, sans-serif;
  background-color: #f5f5f5; /* Light gray background */
}

#app {
  display: flex;
  min-height: 100vh; /* Make the app div span the entire viewport height */
  background-color: #f5f5f5; /* Light gray background */
}
.title-container {
  background-color: red;
  text-align: center;
  padding: 10px 0; /* Adjust vertical padding */
  width: 100%; /* Make the container span the width of the page */
  box-sizing: border-box; /* Include padding in the width calculation */
  position: absolute;
  top: 0;
  left: 0;
  height: 1.2in; /* Set the height to 1 inch */
}

.page-title {
  margin: 0; /* Remove default margin */
  color: black; 
  font-size: 65px;
  font-family: Aptos, Calibri, sans-serif;
  font-weight: 370;
}

.logo {
  position: absolute; /* Position the logo */
  top: 0px; /* Adjust the top position */
  left: 0px; /* Adjust the left position */
  width: 150px; /* Adjust the width of the logo */
  height: auto; /* Maintain aspect ratio */
}

.icon {
  height: 50%;
}

.vertical-nav {
  position: fixed; /* Fix the navigation section */
  top: 0; /* Align it to the top of the viewport */
  left: 0; /* Align it to the left of the viewport */
  height: 100vh; /* Make it span the entire viewport height */
  width: 150px;
  background-color: #f0f0f0;
  padding: 20px;
  box-shadow: 2px 0 5px rgba(0, 0, 0, 0.1);
}

.vertical-nav button {
  display: block;
  width: 100%;
  padding: 10px;
  margin-top: 150px;
  margin-bottom: 0px;
  text-align: left;
  border: none;
  background-color: #fff;
  cursor: pointer;
  transition: background-color 0.3s;
}

.vertical-nav button:hover {
  background-color: #e0e0e0;
}

.main-content {
  margin-left: 10px; /* Adjust the left margin to accommodate the navigation */
  margin-top: 125px;
  flex: 1;
  padding: 20px;
}

.large-buttons button:first-child {
  margin-right: 20px; 
}


.large-buttons {
  display: flex;
  justify-content: space-between;
  margin-bottom: 20px;
  margin-top: 50px;
}

.large-buttons button {
  flex: 1;
  padding: 10px 10px;
  font-size: 35px;
  background-color: #ff7575;
  color: #fff;
  border: 2px solid black;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.large-buttons button:hover {
  background-color: red;
}
/* START SECTION FOR INVENTORY */
/* Add specific styles for the view inventory page */
.inventory-list {
  display: flex;
  flex-wrap: wrap;
}
.inventory-title {
  color: black; /* Set font color to black */
}
.inventory-item {
  width: 300px;
  margin-bottom: 20px;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  color: black; /* Set font color to black */
}
.inventory-table th,
.inventory-table td {
  color: black;
}
/* END SECTION FOR INVENTORY */
</style>
