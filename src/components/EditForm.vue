<template>
  <form class="form" @submit.prevent="updateSensor">
    <h3 class="form__title">Обновить датчик</h3>
    <label v-if="errors.name" for="name" class="form__label">{{
      errors.name
    }}</label>
    <my-input
      v-model="sensorData.name"
      id="name"
      class="form__input"
      placeholder="Имя события"
    />
    <label v-if="errors.temperature" for="temperature" class="form__label">{{
      errors.temperature
    }}</label>
    <my-input
      v-model="sensorData.temperature"
      id="temperature"
      class="form__input"
      placeholder="Температура"
    />
    <label v-if="errors.humidity" for="humidity" class="form__label">{{
      errors.humidity
    }}</label>
    <my-input
      v-model="sensorData.humidity"
      id="humidity"
      class="form__input"
      placeholder="Влажность"
    />
    <my-button class="btn" type="submit">Сохранить</my-button>
  </form>
</template>

<script>
export default {
  props: {
    sensor: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      sensorData: {
        name: this.sensor.name,
        temperature: this.sensor.temperature || "",
        humidity: this.sensor.humidity || "",
      },
      errors: {},
    };
  },

  methods: {
    updateSensor() {
      this.errors = {};

      if (this.sensorData.name === "") {
        this.errors.name = "Введите имя объекта";
      }

      if (this.sensorData.temperature !== "") {
        if (!this.isNumber(this.sensorData.temperature)) {
          this.errors.temperature = "Неверный формат температуры";
        }
      }

      if (this.sensorData.humidity !== "") {
        if (
          !this.isNumber(this.sensorData.humidity) ||
          this.sensorData.humidity < 0 ||
          this.sensorData.humidity > 100
        ) {
          this.errors.humidity = "Неверный данные влажности";
        }
      }

      if (Object.keys(this.errors).length > 0) {
        return;
      }

      let temperature = this.sensorData.temperature.replace("+", "");
      temperature = temperature.replace(",", ".");

      let humidity = this.sensorData.humidity.replace("+", "");
      humidity = humidity.replace(",", ".");

      const newSensor = {
        sensor_id: this.sensor.sensor_id,
        name: this.sensorData.name,
        temperature,
        humidity,
      };

      this.$emit("update", newSensor);
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
