<template>
  <div class="spinner-container">
    <svg :width="size" :height="size" viewBox="0 0 100 100" xmlns="http://www.w3.org/2000/svg">
      <circle cx="50" cy="50" r="42" />
    </svg>
  </div>
</template>

<style lang="scss" scoped>
.spinner-container {
  display: flex;
  align-items: center;
  justify-content: center;
  svg {
    height: 5rem;
    animation: 2s linear infinite svg-animation;
  }

  circle {
    animation: 1.4s ease infinite circle-animation;
    display: block;
    fill: transparent;
    stroke: #2f3d4c;
    stroke-linecap: round;
    stroke-dasharray: 283;
    stroke-width: 10px;
    transform-origin: 50% 50%;
  }
}

@keyframes svg-animation {
  0% {
    transform: rotateZ(0deg);
  }
  100% {
    transform: rotateZ(360deg);
  }
}

@keyframes circle-animation {
  0% {
    stroke-dashoffset: 280;
    transform: rotate(0);
  }

  50% {
    stroke-dashoffset: 75;
    transform: rotate(45deg);
  }

  100% {
    stroke-dashoffset: 280;
    transform: rotate(360deg);
  }
}

circle {
  animation: 1.4s ease-in-out infinite both circle--animation;
}
</style>

<script lang="ts">
import Vue from 'vue'
import { Component, Prop } from 'vue-property-decorator'

@Component
export default class Spinner extends Vue {
  @Prop({ type: String, default: '1rem' }) size: string | undefined;
}
</script>
