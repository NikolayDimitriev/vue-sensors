<template>
  <div>
    <h2>Список датчиков</h2>
    <sensor-item v-for="sensor in sensors" :sensor="sensor" :key="sensor.id" />
  </div>
</template>

<script>
import SensorItem from "@/components/SensorItem.vue";
export default {
  components: {
    SensorItem,
  },
  props: {
    sensors: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped></style>
