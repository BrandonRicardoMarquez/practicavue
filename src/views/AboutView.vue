<script setup>
  import { ref } from "vue";

  const counts = ref(0);
</script>


<template>
  <div class="about">
    <button @click="counts++">You clicked me {{ counts }} times.</button>
  </div>
</template>