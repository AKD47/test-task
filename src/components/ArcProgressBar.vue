<template>
  <div>
    <div class="arc-progress-bar"
         :style="{ width: `${diameter}px`, height: `${diameter}px` }">
      <svg viewBox="0 0 100 100">
        <path :d="bgPath"
              :stroke="bgColor"
              :stroke-width="weight"
              fill="none"
              :style="bgStyles"/>
        <path :d="progressPath"
              :stroke="lineColor"
              fill="none"
              stroke-linecap="round"
              :stroke-width="weight"
              :style="progressPathStyles"/>
      </svg>
    </div>
    <div>
      <input v-model="progress" type="number">
      <input v-model="weight" type="number">
      <input v-model="bgColor" type="text">
      <input v-model="lineColor" type="text">
    </div>
  </div>
</template>

<script>
export default {
  name: 'arc-progress-bar',
  props: {
    diameter: { type: Number, default: 300 }, // 1.
    // progress: { type: Number, default: 70 } // 2.
    // maxValue // 3.
    weight: { type: Number, default: 5 }, // weight // 4. ширина
    bgColor: { type: String, default: '#e5e9f2' },// bgColor // 5.
    lineColor: { type: String, default: '#f56c6c' },// lineColor // 6.
    // arcSize // 7. ???
    // угол поворота?? // 8.
    // animate default linear // 9.
    // animateSpeed // 10.
    // отображать progress // 11.
    // позиция счетчика (внутри/снизу) // 12.
  },
  data() {
    return {
      progress: 70,
      offset: 30
    }
  },
  computed: {
    radius() {
      return this.diameter / 2 - this.offset
    },
    perimeter() {
      return 2 * Math.PI * this.radius
    },
    progressPathStyles() {
      return {
        strokeDasharray: `${(this.diameter - 7) * (this.progress / 100) }px, ${this.perimeter}px`,
        strokeDashoffset: '0px',
        transition: 'stroke-dasharray 0.6s ease 0s, stroke 0.6s ease'
      }
    },
    bgStyles() {
      return {
        strokeDasharray: `100px, 0px`,
        strokeDashoffset: '0px',
        // stroke-dasharray: 221.482px, 295.31px;
      // stroke-dashoffset: -36.9137px;
      }
    },
    bgPath() {
      return `M 50 50
              m 0 47
              a 47 47 0 1 1 0 -94
              a 47 47 0 1 1 0 94`
    },
    progressPath() {
      return `M 50 50
              m 0 47
              a 47 47 0 1 1 0 -94
              a 47 47 0 1 1 0 94`
    }
  }
}
</script>

<style scoped lang="scss">
.arc-progress-bar {
}
</style>
