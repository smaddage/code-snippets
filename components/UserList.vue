<template>
    <div>
      <input v-model="search" placeholder="Search user" />
  
      <ul>
        <li v-for="user in filteredUsers" :key="user">
          <UserItem :user="user" @select="selectedUser = user" />
        </li>
      </ul>
  
      <p v-if="selectedUser">
        Selected: {{ selectedUser.name }}
      </p>
    </div>
  </template>
  
  <script setup>
  import { ref, reactive, watch, computed, onMounted } from "vue";
  import UserItem from "./UserItem.vue";
  
  const users = reactive([]);
  const search = ref("");
  let selectedUser = ref(null);
  
  onMounted(async () => {
    const res = await fetch("https://jsonplaceholder.typicode.com/users");
    users.push(...(await res.json()));
  });
  
  const filteredUsers = computed(() => {
    console.log("filtering...");
    return users.filter(u =>
      u.name.toLowerCase().includes(search.value.toLowerCase())
    );
  });
  
  watch(search, (val) => {
    console.log("Search changed:", val);
  });
  </script>