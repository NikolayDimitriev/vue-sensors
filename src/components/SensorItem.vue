<template>
  <div class="sensor">
    <div>
      <div><strong>Название</strong> {{ sensor.name }}</div>
      <div><strong>Температура</strong> {{ sensor.temperature }}</div>
      <div><strong>Влажность</strong> {{ sensor.humidity }}</div>
    </div>
    <div class="sensor__btns">
      <my-button class="btn" @click="$emit('remove', sensor)"
        >Удалить</my-button
      >
    </div>
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
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.btn {
  color: red;
  border: 1px solid red;
}
</style>
