<template>
  <h1>Список датчиков</h1>
  <section v-if="sensors.length > 0">
    <sensor-item
      v-for="sensor in sensors"
      :sensor="sensor"
      :key="sensor.id"
      @remove="$emit('remove', sensor)"
    />
  </section>
  <section v-else class="empty">Список датчиков пуст</section>
</template>

<script>
import SensorItem from "@/components/SensorItem.vue";
export default {
  components: {
    SensorItem,
  },
  emits: ["remove"],
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
