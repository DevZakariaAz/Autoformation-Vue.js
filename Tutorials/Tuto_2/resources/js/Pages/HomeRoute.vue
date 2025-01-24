<script setup>
import axios from "axios";
import { ref } from "vue";

const showModal = ref(false); // Controls modal visibility
const name = ref(""); // Bind name input
const email = ref(""); // Bind email input
const password = ref(""); // Bind password input
const response = ref(null); // Holds the response data
const users = ref([]); // Holds the list of users

// Function to show the modal
const ShowModal = () => {
  showModal.value = true;
};

// Function to close the modal
const closeModal = () => {
  showModal.value = false;
};

// Function to handle form submission
const submitForm = async () => {
  try {
    const res = await axios.post("/submit-form", {
      name: name.value,
      email: email.value,
      password: password.value,
    });
    response.value = res.data; // Assign response data
    users.value.push(response.value); // Add new user to the list
    closeModal(); // Close the modal after submission
  } catch (error) {
    console.error("Error submitting form:", error);
  }
};

// Fetch users when the component is mounted
const fetchUsers = async () => {
  try {
    const res = await axios.get("/get-users");
    users.value = res.data;
  } catch (error) {
    console.error("Error fetching users:", error);
  }
};

fetchUsers(); // Call fetch function on component mount
</script>


<template>
  <div>
    <h2>HOME</h2>
    <router-link to="/test">Take me to Test page</router-link>
    <button @click="ShowModal">Show Modal</button>

    <div v-if="response">
      <p>Name: {{ response.name }}</p>
      <p>Email: {{ response.email }}</p>
      <p>Password: {{ response.password }}</p>
    </div>

    <!-- List of users -->
    <h3>User List</h3>
    <ul>
      <li v-for="(user, index) in users" :key="index">
        <p><strong>Name:</strong> {{ user.name }}</p>
        <p><strong>Email:</strong> {{ user.email }}</p>
        <p><strong>Password:</strong> {{ user.password }}</p>
      </li>
    </ul>

    <!-- Modal -->
    <div v-if="showModal" class="modal-overlay">
      <div class="modal-content">
        <h3>Create New User</h3>
        <form @submit.prevent="submitForm">
          <div class="form-group">
            <label for="name">Name:</label>
            <input v-model="name" type="text" id="name" name="name" required placeholder="Enter your name" />
          </div>
          <div class="form-group">
            <label for="email">Email:</label>
            <input v-model="email" type="email" id="email" name="email" required placeholder="Enter your email" />
          </div>
          <div class="form-group">
            <label for="password">Password:</label>
            <input v-model="password" type="password" id="password" name="password" required
              placeholder="Enter your password" />
          </div>
          <div class="form-actions">
            <button type="submit" class="submit-btn">Submit</button>
            <button type="button" @click="closeModal" class="close-btn">Close</button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.7);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 999;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  max-width: 500px;
  width: 100%;
  display: flex;
  flex-direction: column;
}

h3 {
  text-align: center;
  margin-bottom: 20px;
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 5px;
  font-weight: bold;
}

input {
  width: 100%;
  padding: 8px;
  border-radius: 4px;
  border: 1px solid #ccc;
}

.form-actions {
  display: flex;
  justify-content: space-between;
}

.submit-btn {
  background-color: #4CAF50;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
}

.submit-btn:hover {
  background-color: #45a049;
}

.close-btn {
  background-color: #f44336;
  color: white;
  border: none;
  padding: 10px 20px;
  border-radius: 4px;
  cursor: pointer;
}

.close-btn:hover {
  background-color: #e53935;
}
</style>
