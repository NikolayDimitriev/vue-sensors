<template>
  <div class="modal" v-if="isShow" @click.stop="closeModal">
    <div @click.stop class="modal__content"><slot></slot></div>
  </div>
</template>

<script>
export default {
  name: "my-modal",
  props: {
    isShow: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    closeModal() {
      this.$emit("update:isShow", false);
    },
  },
};
</script>

<style scoped>
.modal {
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}

.modal__content {
  margin: auto;
  background-color: white;
  border-radius: 10px;
  min-height: 50px;
  min-width: 300px;
  padding: 25px;
}
</style>
