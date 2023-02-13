<script setup>
import Alert from "./components/Alert.vue";
import { ref } from "vue";

const showAlert = ref(true);
</script>

<template>
  <div class="space-y-5">
    <Alert
      :show="showAlert"
      :on-dismiss="() => (showAlert = false)"
      title="Awesome Alert"
    >
      <p>Some important message</p>
    </Alert>
    <Alert
      :show="showAlert"
      intent="success"
      :on-dismiss="() => (showAlert = false)"
      title="Awesome Alert"
    >
      <p>Some important message</p>
    </Alert>
    <Alert
      :show="showAlert"
      intent="warning"
      :on-dismiss="() => (showAlert = false)"
      title="Awesome Alert"
    >
      <p>Some important message</p>
    </Alert>
    <Alert
      :show="showAlert"
      intent="danger"
      :on-dismiss="() => (showAlert = false)"
      title="Awesome Alert"
    >
      <p>Some important message</p>
    </Alert>
  </div>
</template>

<style></style>
