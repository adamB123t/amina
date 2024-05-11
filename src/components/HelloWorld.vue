<!-- eslint-disable vue/no-parsing-error -->
<template>
  <div class="custom-table">
    <table>
      <thead>
        <tr>
          <th>USERNAME</th>
          <th>HOURS</th>
          <th>VEHICLE ID</th>
          <th>ACTIONS</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in itemsWithActions" :key="item.username" :class="{ 'accepted': item.actions.accept, 'denied': item.actions.deny }">
          <td>{{ item.username }}</td>
          <td>{{ item.hours }}</td>
          <td>{{ item.vehicleId }}</td>
          <td>
            <td>
  <button @click="() => handleAccept(item)" v-if="!item.actions.accept" class="accept-button">Accept</button>
  <button @click="() => handleDeny(item)" v-if="!item.actions.deny && !item.actions.accept" class="deny-button">Deny</button>
</td>

          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script lang="js" setup>
  import { ref } from 'vue';

  const items = [
    { username: "ahmed.brini@gmail.com", hours: 2, vehicleId: "ABC123", actions: { accept: false, deny: false } },
    { username: "nour.benzarti@gmail.com", hours: 1, vehicleId: "XYZ789", actions: { accept: false, deny: false } },
    // Add more items as needed
  ];

  const itemsWithActions = ref(items);

  const handleAccept = (item) => {
    item.actions.accept = true;
    item.actions.deny = false; // Reset deny status if previously set
  };

  const handleDeny = (item) => {
    item.actions.deny = true;
    item.actions.accept = false; // Reset accept status if previously set

  };
</script>

<style scoped>
  .custom-table {
    margin: 20px;
  }

  table {
    width: 100%;
    border-collapse: collapse;
  }

  th, td {
    border: 1px solid #ddd;
    padding: 8px;
    text-align: left;
  }

  th {
    background-color: #f2f2f2;
  }

  .accepted {
    background-color: #a5d6a7; /* Green background for accepted rows */
  }

  .denied {
    display: none; /* Hide denied rows */
  }

  .accept-button {
    background-color: #4caf50; /* Green background for Accept button */
    color: #fff; /* White text for Accept button */
    padding: 5px 10px;
    margin-right: 5px;
  }

  .deny-button {
    background-color: #f44336; /* Red background for Deny button */
    color: #fff; /* White text for Deny button */
    padding: 5px 10px;
    margin-right: 5px;
  }
</style>
