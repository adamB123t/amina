<template>
  <div>
    <v-app-bar>
      <v-toolbar-title style="font-size: 30px; font-family: 'League Spartan', sans-serif; font-weight: bold;">EcoRide</v-toolbar-title>
      <v-spacer></v-spacer>
      <v-btn @click="showAddDialog = true">Add</v-btn>
      <v-btn to="/landing">Return to stores</v-btn>
      <v-btn to="/landing">Log Out</v-btn>
      <v-menu open-on-hover>
        <!-- Your menu content goes here -->
      </v-menu>
    </v-app-bar>

    <!-- Dialog for adding vehicles -->
    <v-dialog v-model="showAddDialog" max-width="500px">
      <v-card>
        <v-card-title>Add Vehicle</v-card-title>
        <v-card-text>
          <!-- Form for adding vehicles -->
          <v-form @submit.prevent="addVehicles">
            <v-text-field v-model="newVehicle.price" label="Price per Hour"></v-text-field>
            <v-text-field v-model="numToAdd" type="number" label="Number of Vehicles to Add"></v-text-field>
            <v-btn type="submit">Add</v-btn>
          </v-form>
        </v-card-text>
      </v-card>
    </v-dialog>

    <!-- Table view for displaying vehicles -->
    <v-data-table :headers="headers" :items="vehicles" hide-actions>
      <template v-slot:top>
        <thead>
          <tr>
            <th>Status</th>
            <th style="padding-left: 750px;">Price per Hour</th> <!-- Add padding between headers -->
          </tr>
        </thead>
      </template>
      <template v-slot:items="props">
        <td>{{ props.item.status }}</td>
        <td>{{ props.item.price }}</td>
        <td>
          <v-btn @click="clonePrice(props.item)">Clone Price</v-btn>
          <v-btn @click="cloneStatus(props.item)">Clone Status</v-btn>
        </td>
      </template>
    </v-data-table>
  </div>
</template>
<script>
export default {
  data() {
    return {
      showAddDialog: false,
      numToAdd: 1, // Number of vehicles to add at once
      newVehicle: {
        price: '' // Price per hour
      },
      vehicles: [], // Array to store vehicles
      headers: [
        { text: 'Status', value: 'status' },
        { text: 'Price per Hour', value: 'price' },
        { text: 'Actions', value: 'actions' },
        // Add more headers as needed
      ]
    };
  },
  methods: {
    addVehicles() {
      for (let i = 0; i < this.numToAdd; i++) {
        // Push new vehicles to the vehicles array
        this.vehicles.push({ status: 'Available', price: this.newVehicle.price });
      }
      // Clear the newVehicle object
      this.newVehicle.price = '';
      // Close the dialog
      this.showAddDialog = false;
    },
    clonePrice(item) {
      // Clone the price of the selected item and add it to the vehicles array
      this.vehicles.push({ status: item.status, price: item.price });
    },
    cloneStatus(item) {
      // Clone the status of the selected item and add it to the vehicles array
      this.vehicles.push({ status: item.status, price: this.newVehicle.price });
    }
  }
};
</script>
