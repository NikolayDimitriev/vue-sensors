<template>
  <article class="sensor">
    <div>
      <div><b>ID датчика:</b> {{ sensor.sensor_id }}</div>
      <div><b>Имя событий:</b> {{ sensor.name }}</div>
      <div v-if="sensor.temperature">
        <b>Температура:</b> {{ sensor.temperature }}°C
      </div>
      <div v-if="sensor.humidity"><b>Влажность:</b> {{ sensor.humidity }}%</div>
    </div>
    <div class="sensor__btns">
      <my-button class="btn" @click="$emit('remove', sensor)"
        >Удалить</my-button
      >
    </div>
  </article>
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
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.btn {
  color: red;
  border: 1px solid red;
}
</style>
