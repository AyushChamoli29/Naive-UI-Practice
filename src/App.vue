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
  </n-message-provider>
</template>
