<script setup>
import { ref } from "vue";

const todo = ref("");
</script>

<template>
  <h1 class="my-14 w-[660px] h-[70px] bg-backgroundThin flex items-center">
    <input
      type="text"
      class="w-full h-full px-5 text-2xl border-none bg-backgroundThin text-white"
      placeholder="What needs to be done?"
    />
    <button class="w-32 h-full bg-green text-white">Add</button>
  </h1>
</template>
