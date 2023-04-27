<template>
  <form class="form" @submit.prevent="createNewSensor">
    <h3 class="form__title">Добавить новый датчик</h3>
    <my-input
      v-model="sensor.name"
      class="form__input"
      placeholder="Имя события"
    />
    <label v-if="errors.temperature" for="temperature" class="form__label">{{
      errors.temperature
    }}</label>
    <my-input
      v-model="sensor.temperature"
      id="temperature"
      class="form__input"
      placeholder="Температура"
    />
    <label v-if="errors.humidity" for="humidity" class="form__label">{{
      errors.humidity
    }}</label>
    <my-input
      v-model="sensor.humidity"
      id="humidity"
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
      errors: {},
    };
  },

  methods: {
    createNewSensor() {
      this.errors = {};

      if (
        this.sensor.temperature !== "" &&
        !this.isNumber(this.sensor.temperature)
      ) {
        this.errors.temperature = "Неверный формат температуры";
      }

      if (
        (this.sensor.humidity !== "" && !this.isNumber(this.sensor.humidity)) ||
        this.sensor.humidity < 0 ||
        this.sensor.humidity > 100
      ) {
        this.errors.humidity = "Неверный данные влажности";
      }

      if (Object.keys(this.errors).length > 0) {
        return;
      }

      let temperature = this.sensor.temperature.replace("+", "");
      temperature = temperature.replace(",", ".");

      let humidity = this.sensor.humidity.replace("+", "");
      humidity = humidity.replace(",", ".");

      const newSensor = {
        sensor_id: Date.now(),
        name: this.sensor.name || "N/A",
        temperature,
        humidity,
      };

      this.$emit("create", newSensor);

      this.sensor = {
        name: "",
        temperature: "",
        humidity: "",
      };
    },
    isNumber(field) {
      const reg = new RegExp(/^[+-]?\d+([.,]?\d+)?$/);
      return reg.test(field);
    },
  },
};
</script>

<style scoped>
.form {
  display: flex;
  flex-direction: column;
  max-width: 350px;
}

.form__title {
  margin-bottom: 15px;
}

.form__input {
  width: 100%;
  margin-bottom: 15px;
}

.form__label {
  color: red;
}

.btn {
  align-self: center;
  background-color: #3369f3;
  color: white;
  border: 1px solid #3369f3;
}
</style>
