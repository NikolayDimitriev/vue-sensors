<template>
  <form class="form" @submit.prevent="createNewSensor">
    <h3>Добавить новый датчик</h3>
    <my-input
      v-model="sensor.name"
      class="form__input"
      placeholder="Название"
    />
    <my-input
      v-model="sensor.temperature"
      class="form__input"
      placeholder="Температура"
    />
    <my-input
      v-model="sensor.humidity"
      class="form__input"
      placeholder="Влажность"
    />
    <my-button class="btn" type="submit">Добавить</my-button>
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

.form__input {
  width: 100%;
  margin-top: 15px;
}

.btn {
  margin-top: 15px;
  align-self: flex-end;
  border: 1px solid teal;
}
</style>
