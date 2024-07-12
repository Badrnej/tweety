<template>
    <div class="border p-4">
      <h3>Suggestions</h3>
      <ul>
        <li v-for="user in users" :key="user.id">{{ user.username }}</li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    name: 'UserSuggestions',
    data() {
      return {
        users: []
      }
    },
    created() {
      fetch('http://localhost:3000/users')
        .then(response => response.json())
        .then(data => this.users = data);
    }
  }
  </script>
  