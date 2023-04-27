<template>
  <div class="container">
    <sensor-form @create="createNewSensor"></sensor-form>
    <sensor-list :sensors="sensors" @remove="removeSensor"></sensor-list>
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
    };
  },

  methods: {
    createNewSensor(sensor) {
      this.sensors.push(sensor);
      this.updateLocalStorage();
    },

    removeSensor(sensor) {
      this.sensors = this.sensors.filter(
        (s) => s.sensor_id !== sensor.sensor_id
      );
      this.updateLocalStorage();
    },
    updateLocalStorage() {
      const parsed = JSON.stringify(this.sensors);
      localStorage.setItem("data", parsed);
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
  padding: 20px;
}
</style>
