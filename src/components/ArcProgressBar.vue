<template>
  <div class="arc-progress-bar"
       :style="{ width: `${diameter}px`, height: `${diameter}px` }">
    <svg viewBox="0 0 100 100">
      <path d="M 50 50
               m 0 47
               a 47 47 0 1 1 0 -94
               a 47 47 0 1 1 0 94"
            :stroke="bgColor"
            :stroke-width="weight"
            fill="none"
            :style="bgStyles"/>
      <path d="M 50 50
               m 0 47
               a 47 47 0 1 1 0 -94
               a 47 47 0 1 1 0 94"
            :stroke="lineColor"
            fill="none"
            stroke-linecap="round"
            :stroke-width="weight"
            :style="progressPathStyles"/>
    </svg>
    <div class="arc-progress-bar__value"
         :style="counterStyles">
      <span>{{ value }}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'arc-progress-bar',
  props: {
    diameter: { type: Number, default: 300 }, // 1.
    progress: { type: Number, default: 70 }, // 2.
    maxProgress: { type: Number, default: 100 }, // maxValue // 3.
    weight: { type: Number, default: 5 }, // weight // 4. ширина
    bgColor: { type: String, default: '#e5e9f2' },// bgColor // 5.
    lineColor: { type: String, default: '#f56c6c' },// lineColor // 6.
    visiblePartOfCircle: { type: Number, default: 100 }, // 7.
    // угол поворота?? // 8.
    // animate default linear // 9.
    // animateSpeed // 10.
    // +++++ отображать progress // 11. +++++
    counterPosition: { type: String, default: 'center' }, // center or bottom // 12.
  },
  computed: {
    value() {
      if (this.maxProgress === 100 || this.progress < this.maxProgress) {
        return this.progress
      } else {
        return this.maxProgress
      }
    },
    perimeter() {
      return Math.PI * this.diameter
    },
    progressPathStyles() {
      const offset = (100 - this.visiblePartOfCircle) / 2
      const dashoffset = (offset / 100) * 295
      const dasharray = 295 - (dashoffset * 2)
      return {
        strokeDasharray: `${dasharray * this.value / 100}, ${this.perimeter}`,
        strokeDashoffset: -dashoffset,
        transition: 'stroke-dasharray 0.6s ease 0s, stroke 0.6s ease'
      }
    },
    bgStyles() {
      const offset = (100 - this.visiblePartOfCircle) / 2
      const dashoffset = (offset / 100) * 295
      const dasharray = 295 - (dashoffset * 2)
      return {
        strokeDasharray: `${dasharray}, ${this.perimeter}`,
        strokeDashoffset: -dashoffset
      }
    },
    counterStyles() {
      if (this.counterPosition === 'center') {
        if (this.visiblePartOfCircle > 60) {
          return null
        } else {
          const topOffset = ((this.diameter + 20) / 2) * (this.visiblePartOfCircle / 100)
          return {
            bottom: 'unset',
            top: `${topOffset}px`
          }
        }
      } else {
        let bottomOffset = '0px'
        if (this.visiblePartOfCircle > 85) {
          bottomOffset = '-30px'
        } else if (this.visiblePartOfCircle > 65) {
          bottomOffset = `${100 - (this.visiblePartOfCircle + 20)}%`
        } else {
          bottomOffset = `${100 - (this.visiblePartOfCircle)}%`
        }
        return {
          top: 'unset',
          bottom: bottomOffset
        }
      }
    },
  }
}
</script>

<style scoped lang="scss">
.arc-progress-bar {
  position: relative;

  &__value {
    position: absolute;

    margin: 0;
    top: 0; bottom: 0;
    left: 0; right: 0;

    display: flex;
    justify-content: center;
    align-items: center;

    > span {
      font-size: 18px;
      font-weight: 600;
    }

  }

}
</style>
