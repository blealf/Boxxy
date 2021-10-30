<template>
  <div>
    <button
      class="show-color-picker"
      @click="showColorPicker = !showColorPicker"
    >
      {{ showColorPicker ? 'Apply' : 'Change color' }}
    </button>
    <div
      v-if="showColorPicker"
      :style="{ background: color }"
      class="color-picker"
      @blur="showColorPicker = !showColorPicker"
    >
      <ColorPicker
        theme="light"
        :color="color"
        :sucker-hide="showColorPicker"
        :sucker-canvas="suckerCanvas"
        :sucker-area="suckerArea"
        @changeColor="changeColor"
        @openSucker="openSucker"
      />
    </div>
  </div>
</template>

<script>
import { ColorPicker } from 'vue-color-kit';
import 'vue-color-kit/dist/vue-color-kit.css';

export default {
  components: {
    ColorPicker,
  },
  data() {
    return {
      color: '#fff',
      showColorPicker: false,
    };
  },
  methods: {
    changeColor(color) {
      const { r, g, b, a } = color.rgba;
      this.color = `rgba(${r}, ${g}, ${b}, ${a})`;
      this.$emit('change-color', this.color);
    },
    openSucker(isOpen) {
      if (isOpen) {
        // ... canvas be created
        // this.suckerCanvas = canvas
        // this.suckerArea = [x1, y1, x2, y2]
      } else {
        // this.suckerCanvas && this.suckerCanvas.remove
      }
    },
  },
};
</script>

<style scoped>
.show-color-picker {
  padding: 10px;
  font-size: 1.1rem;
  border: none;
  background: #c63b3b;
  color: #fff;
  cursor: pointer;
  border-radius: 5px;
}
.color-picker {
  width: 200px;
  margin-top: -45px;
  margin-left: 70px;
}
</style>
