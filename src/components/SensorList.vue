<template>
  <h2>Список датчиков</h2>
  <div v-if="sensors.length > 0">
    <sensor-item
      v-for="sensor in sensors"
      :sensor="sensor"
      :key="sensor.id"
      @remove="$emit('remove', sensor)"
    />
  </div>
  <div v-else class="empty">Список датчиков пуст</div>
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

<style scoped>
.empty {
  width: 100%;
  height: 200px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
