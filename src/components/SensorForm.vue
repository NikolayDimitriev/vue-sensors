<template>
  <form class="form" @submit.prevent="createNewSensor">
    <h3>Добавить новый датчик</h3>
    <input
      v-model="sensor.name"
      class="input"
      type="text"
      placeholder="Название"
    />
    <input
      v-model="sensor.temperature"
      class="input"
      type="number"
      placeholder="Температура"
    />
    <input
      v-model="sensor.humidity"
      class="input"
      type="number"
      placeholder="Влажность"
    />
    <button class="button" type="submit">Добавить</button>
  </form>
</template>

<script>
export default {
  data() {
    return {
      sensor: {
        name: "",
        temperature: "",
        humidity: "",
      },
    };
  },

  methods: {
    createNewSensor() {
      this.sensor.id = Date.now();

      this.$emit("create", this.sensor);

      this.sensor = {
        name: "",
        temperature: "",
        humidity: "",
      };
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
  border-radius: 10px;
}

.button {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  border: 1px solid teal;
  border-radius: 10px;
}
</style>
