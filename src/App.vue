<script setup lang="ts">
import one from "./one.vue";
import { NMessageProvider } from "naive-ui";
import Two from "./two.vue";
</script>

<template>
  <n-message-provider>
    <one />
    <two />
    <p>Hello everyone!</p>
    <p>My name is Ayush</p>
    <p>I am an intern in travelexic.</p>
  </n-message-provider>
</template>
