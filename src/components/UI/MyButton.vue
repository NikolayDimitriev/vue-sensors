<template>
  <button class="button"><slot></slot></button>
</template>

<script>
export default {
  name: "my-button",
};
</script>

<style scoped>
.button {
  padding: 10px 15px;
  border-radius: 10px;
  outline: none;
  border: none;
}

@media (min-width: 992px) {
  .button {
    cursor: pointer;
  }
}
</style>
