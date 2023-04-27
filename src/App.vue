<template>
  <div class="app">
    <sensor-form @create="createNewSensor"></sensor-form>
    <sensor-list :sensors="sensors"></sensor-list>
  </div>
</template>

<script>
import SensorForm from "@/components/SensorForm.vue";
import SensorList from "@/components/SensorList.vue";

export default {
  components: {
    SensorForm,
    SensorList,
  },
  data() {
    return {
      sensors: [
        { sensor_id: 1, name: "JavaScript", temperature: 20, humidity: 25 },
        { sensor_id: 2, name: "TypeScript", temperature: 20, humidity: 25 },
        { sensor_id: 3, name: "Vue", temperature: 20, humidity: 25 },
      ],
    };
  },

  methods: {
    createNewSensor(sensor) {
      this.sensors.push(sensor);
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
