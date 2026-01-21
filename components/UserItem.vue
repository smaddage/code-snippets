<template>
    <div @click="selectUser">
      <p>{{ user.name }}</p>
      <p>{{ user.Email }}</p>
      <span v-html="user.description"></span>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    user: Object
  });
  
  const emit = defineEmits(["select"]);
  
  function selectUser() {
    emit("select", props.user);
  }
  </script>