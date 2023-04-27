<template>
  <section v-if="sensors.length > 0" class="sensor">
    <sensor-item
      v-for="sensor in sensors"
      :sensor="sensor"
      :key="sensor.id"
      @remove="$emit('remove', sensor)"
      @openModal="handleModal"
    />
    <my-modal v-model:isShow="isModalShow">
      <edit-form :sensor="openedSensor" @update="updateSensor"></edit-form>
    </my-modal>
  </section>
  <section v-else class="empty">Список датчиков пуст</section>
</template>

<script>
import SensorItem from "@/components/SensorItem.vue";
import EditForm from "@/components/EditForm.vue";
export default {
  components: {
    SensorItem,
    EditForm,
  },
  emits: ["remove", "openModal", "update"],
  props: {
    sensors: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      isModalShow: false,
      openedSensor: null,
    };
  },
  methods: {
    handleModal(sensor) {
      this.openedSensor = sensor;
      this.isModalShow = !this.isModalShow;
    },
    updateSensor(sensor) {
      this.$emit("update", sensor);
      this.handleModal(null);
    },
  },
};
</script>

<style scoped>
.sensor {
  padding: 15px 0;
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

@media (max-width: 600px) {
  .sensor {
    display: flex;
    flex-direction: column;
  }
}
.empty {
  width: 100%;
  height: 100px;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
