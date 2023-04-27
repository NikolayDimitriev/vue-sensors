<template>
  <div class="sensor">
    <div><strong>Name</strong> {{ sensor.name }}</div>
    <div><strong>Temperature</strong> {{ sensor.temperature }}</div>
    <div><strong>Humidity</strong> {{ sensor.humidity }}</div>
  </div>
</template>

<script>
export default {
  props: {
    sensor: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.sensor {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}
</style>
