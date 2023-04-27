<template>
  <div class="container">
    <header class="header">
      <h1 class="header__title">Список датчиков</h1>
      <my-button class="header__btn" @click="showModal">Добавить</my-button>
    </header>

    <my-modal v-model:isShow="isModalShow">
      <sensor-form @create="createNewSensor"></sensor-form>
    </my-modal>
    <sensor-list
      :sensors="sensors"
      @remove="removeSensor"
      @update="updateSensor"
    ></sensor-list>
  </div>
</template>

<script>
import SensorForm from "@/components/SensorForm.vue";
import SensorList from "@/components/SensorList.vue";
import sensorsData from "@/mock/events.json";

export default {
  components: {
    SensorForm,
    SensorList,
  },
  data() {
    return {
      sensors: [],
      isModalShow: false,
    };
  },

  methods: {
    createNewSensor(sensor) {
      this.sensors.push(sensor);
      this.isModalShow = false;
      this.updateLocalStorage();
    },

    removeSensor(sensor) {
      this.sensors = this.sensors.filter(
        (s) => s.sensor_id !== sensor.sensor_id
      );
      this.updateLocalStorage();
    },
    updateSensor(sensor) {
      this.sensors = this.sensors.map((s) => {
        if (s.sensor_id === sensor.sensor_id) {
          return sensor;
        }
        return s;
      });
      this.updateLocalStorage();
    },
    updateLocalStorage() {
      const parsed = JSON.stringify(this.sensors);
      localStorage.setItem("data", parsed);
    },
    showModal() {
      this.isModalShow = true;
    },
  },
  mounted() {
    if (localStorage.getItem("data")) {
      try {
        this.sensors = JSON.parse(localStorage.getItem("data"));
      } catch (e) {
        localStorage.removeItem("data");
        this.sensors = sensorsData;
      }
    } else {
      this.sensors = sensorsData;
    }
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  width: 95%;
  margin: 0 auto;
  padding: 15px 0;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.header__title {
  display: inline-block;
  margin-right: 15px;
}

.header__btn {
  background-color: #3369f3;
  color: white;
}

@media (max-width: 600px) {
  .header__title {
    font-size: 24px;
  }
}
</style>
