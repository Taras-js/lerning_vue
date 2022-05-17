<template>
  <div v-if="show" class="dialog" @click.stop="hideDialog">
    <div @click.stop class="dialog__container">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    show: {
      type: Boolean,
      default: false
    }

  },
  methods: {
    hideDialog() {
      this.$emit('update:show',false )
    }
  }
}
</script>

<style scoped>
.dialog {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}
.dialog__container {
  margin: auto;
  background: white;
  border-radius: 12px;
  min-height: 300px;
  min-width: 400px;
  padding: 20px;
}
</style>