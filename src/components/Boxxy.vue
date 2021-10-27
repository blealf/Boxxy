<template>
  <div class="boxxy">
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

    <!-- Sliders -->
    <div class="sliders">
      <!-- Horizontal -->
      <h3>Horizontal shadow: {{ horizontal }}</h3>
      <Slider
        v-model="horizontal"
        :min="min"
        :max="max"
        class="slider"
        tooltips
        showTooltip="focus"
        :style="{
          '--slider-connect-bg': `${boxColor}`,
          '--slider-tooltip-bg': `${boxColor}`,
        }"
      ></Slider>
      <!-- Veritcal -->
      <h3>Vertical shadow: {{ vertical }}</h3>
      <Slider
        v-model="vertical"
        :min="min"
        :max="max"
        class="slider"
        tooltips
        showTooltip="focus"
        :style="{
          '--slider-connect-bg': `${boxColor}`,
          '--slider-tooltip-bg': `${boxColor}`,
        }"
      ></Slider>
      <!-- Blur -->
      <h3>blur: {{ blur }}</h3>
      <Slider
        v-model="blur"
        class="slider"
        tooltips
        showTooltip="focus"
        :style="{
          '--slider-connect-bg': `${boxColor}`,
          '--slider-tooltip-bg': `${boxColor}`,
        }"
      />
      <!-- Spread -->
      <h3>spread: {{ spread }}</h3>
      <Slider
        v-model="spread"
        :min="min"
        :max="max"
        class="slider"
        tooltips
        showTooltip="focus"
        :style="{
          '--slider-connect-bg': `${boxColor}`,
          '--slider-tooltip-bg': `${boxColor}`,
        }"
      ></Slider>
      <!-- Opacity -->
      <h3>Opacity: {{ opacity }}</h3>
      <Slider
        v-model="opacity"
        :min="0.05"
        :max="0.99"
        :step="-1"
        class="slider"
        tooltips
        showTooltip="focus"
        :style="{
          '--slider-connect-bg': `${boxColor}`,
          '--slider-tooltip-bg': `${boxColor}`,
        }"
      ></Slider>
    </div>

    <!-- The Box -->
    <div
      class="box-shadow"
      :style="{
        'background-color': `${boxColor}`,
        'box-shadow': `${horizontal}px ${vertical}px ${blur}px ${spread}px ${color}`,
      }"
    >
      {{ `box-shadow: ${horizontal}px ${vertical}px ${5}px ${0}px ${color}` }}
    </div>
    {{ color }}
  </div>
</template>

<script>
import Slider from '@vueform/slider';
import { ColorPicker } from 'vue-color-kit';
import 'vue-color-kit/dist/vue-color-kit.css';
import '@vueform/slider/themes/default.css';

export default {
  name: 'Boxxy',
  components: {
    Slider,
    ColorPicker,
  },
  data() {
    return {
      horizontal: 10,
      vertical: 10,
      blur: 10,
      spread: 0,
      min: -190,
      max: 190,
      opacity: 0.5,
      inset: false,
      color: 'rgba(34, 31, 26, 0.8)',
      boxColor: 'rgba(59, 198, 198, 0.8)',
      showColorPicker: false,
      suckerCanvas: null,
      suckerArea: [],
      isSucking: false,
    };
  },
  watch: {
    opacity(value) {
      const rm = this.color
        .replace('rgba(', '')
        .replace(')', '')
        .replace(' ', '')
        .split(',');
      this.color = `rgba(${Number(rm[0])}, ${Number(rm[1])}, ${Number(
        rm[2]
      )}, ${value})`;
    },
  },
  methods: {
    changeColor(color) {
      const { r, g, b, a } = color.rgba;
      this.color = `rgba(${r}, ${g}, ${b}, ${a})`;
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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.boxxy {
  padding: calc(10% - 20px);
  width: 100%;
  box-sizing: border-box;
  position: relative;
}
.show-color-picker {
  position: absolute;
  right: 20px;
  padding: 10px;
  font-size: 1.1rem;
  border: none;
  background: #c63b3b;
  color: #d9d0d0;
  cursor: pointer;
}
.color-picker {
  position: absolute;
  right: 20px;
  margin-top: 45px;
  z-index: 2;
}
.sliders {
  margin-top: 50px;
}
.box-shadow {
  margin: 0 auto;
  margin-top: calc(10vw - 10px);
  height: 300px;
  width: 80%;
  min-width: 300px;
  background-color: green;
  border-radius: 20px;
  padding: 20px;
}
</style>
