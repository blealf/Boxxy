<template>
  <div class="toggle" @click="$emit('update', !toggle)">
    <div
      class="switch"
      :style="{
        'margin-left': toggle ? '55px' : '0px',
        opacity: toggle ? '1' : '0.5',
      }"
    ></div>
  </div>
</template>

<script>
export default {
  props: {
    toggle: {
      type: Boolean,
      default: false,
    },
  },
};
</script>

<style scoped>
.toggle {
  width: 100px;
  height: 35px;
  border-radius: 5px;
  padding: 5px;
  box-shadow: 1px 1px 5px 0px rgba(34, 31, 26, 0.35) inset;
  background: teal;
  cursor: pointer;
}
.switch {
  position: relative;
  height: 100%;
  width: 45px;
  border-radius: 2px;
  background: red;
  transition: all 300ms ease-in-out;
}
.switch::after {
  content: '|||';
  font-size: 28px;
  position: absolute;
  right: 2px;
  color: grey;
}
</style>
