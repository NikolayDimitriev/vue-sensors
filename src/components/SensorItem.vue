<template>
  <article class="sensor__item">
    <div class="sensor__info">
      <div><b>ID датчика:</b> {{ sensor.sensor_id }}</div>
      <div><b>Имя событий:</b> {{ sensor.name }}</div>
      <div v-if="sensor.temperature">
        <b>Температура:</b> {{ sensor.temperature }}°C
      </div>
      <div v-if="sensor.humidity"><b>Влажность:</b> {{ sensor.humidity }}%</div>
    </div>
    <div class="sensor__btns">
      <my-button class="btn--edit" @click="$emit('openModal', sensor)"
        >Редактировать</my-button
      >
      <my-button class="btn" @click="$emit('remove', sensor)"
        >Удалить</my-button
      >
    </div>
    <slot></slot>
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
.sensor__item {
  padding: 15px;
  border: 2px solid teal;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  min-width: 260px;
}

.sensor__info {
  align-self: flex-start;
}

.sensor__btns {
  width: 100%;
  margin-top: 10px;
}

.sensor__btns {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.btn {
  color: white;
  background-color: red;
}

.btn--edit {
  color: white;
  background-color: #3369f3;
}
</style>
