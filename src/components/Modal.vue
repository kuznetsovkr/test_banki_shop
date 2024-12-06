<script>
export default {
  name: "Modal",
  methods: {
    close() {
      this.$emit("close");
    },
  },
};
</script>


<template>
  <div class="modal-backdrop" @click.self="close">
    <div class="modal-window">
      <button class="modal-close" @click="close">×</button>
      <slot></slot>
    </div>
  </div>
</template>
