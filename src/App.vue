<template>
  <div class="app">
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
      sensors: sensorsData,
    };
  },

  methods: {
    createNewSensor(sensor) {
      this.sensors.push(sensor);
    },

    removeSensor(sensor) {
      this.sensors = this.sensors.filter(
        (s) => s.sensor_id !== sensor.sensor_id
      );
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
</style>
