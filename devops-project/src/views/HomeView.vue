<script setup>
import { ref } from 'vue';

const users = ref([]);

const fetchUsers = async () => {
  try {
    const response = await fetch('http://localhost:3000/users');
    if (!response.ok) throw new Error('Failed to fetch users');
    users.value = await response.json();
  } catch (error) {
    console.error(error);
    alert('Could not load users. Please try again later.');
  }
};
</script>

<template>
  <div>
    <header>
      <h1>User List Application</h1>
    </header>
    <main>
      <button @click="fetchUsers">Load Users</button>
      <ul>
        <li v-for="user in users" :key="user.id">
          <strong>{{ user.name }}</strong> ({{ user.email }})
        </li>
      </ul>
    </main>
  </div>
</template>

<style scoped>
header {
  background-color: #007BFF;
  color: white;
  padding: 1rem;
  text-align: center;
}

header h1 {
  margin: 0;
}

main {
  padding: 20px;
  text-align: center;
}

ul {
  list-style: none;
  padding: 0;
}

li {
  background-color: #f1f1f1;
  margin: 10px auto;
  color: #000000;
  padding: 10px;
  border-radius: 5px;
  max-width: 400px;
}

button {
  background-color: #007BFF;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background-color: #0056b3;
}
</style>
