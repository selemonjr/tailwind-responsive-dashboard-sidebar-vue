<script setup>
import Sidebar from "./components/Sidebar.vue";
import { RouterView } from "vue-router";
</script>
<template>
  <div class="flex font-sans text-white bg-gray-900">
        <div class="absolute z-1 top-2 left-3 md:left-20 pl-2">
    <h1 class="text-center font-bold text-xl">Sidebar</h1>
    </div>
    <div class="flex flex-col w-0 min-h-screen md:w-80 bg-gray-900 md:border-2 md:border-text-white pt-10">
      <Sidebar />
    </div>
    <RouterView/>
  </div>
</template>