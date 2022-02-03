<template>
  <div class="task1">
    <div class="task1__content">
      <list :list="leftColumnCards"
            @got-to-bottom="loadCards(20)"
            @move-card="moveToRight"
            @show-tooltip="showTooltip"
            @hide-tooltip="hideTooltip"
            ref="list"/>
      <list :list="rightColumnCards"
            @move-card="moveToLeft"
            @show-tooltip="showTooltip"
            @hide-tooltip="hideTooltip"/>
    </div>
    <tooltip ref="tooltip"/>
  </div>
</template>

<script>
import Tooltip from "./Tooltip";
import List from "@/views/task1/List";

export default {
  name: "task1",
  components: { Tooltip, List },
  data() {
    return {
      totalCardsCount: 10000,
      loadedCardsCount: 0,
      leftColumnCards: [],
      rightColumnCards: []
    }
  },
  mounted() {
    this.loadCards(40)
  },
  methods: {
    showTooltip({$event, card}) {
      this.$refs.tooltip.show(card)
      this.$refs.tooltip.setPosition($event.target)
    },
    hideTooltip() {
      this.$refs.tooltip.hide()
    },
    moveToRight(index) {
      this.hideTooltip()
      const card = this.leftColumnCards[index]
      this.leftColumnCards.splice(index, 1)
      this.rightColumnCards.push(card)
      this.$refs.list.handleScroll(null)
    },
    moveToLeft(index) {
      this.hideTooltip()
      const card = this.rightColumnCards[index]
      this.rightColumnCards.splice(index, 1)
      this.leftColumnCards.push(card)
      this.$refs.list.handleScroll(null)
    },
    loadCards(cardsCount = 20) {
      if (this.loadedCardsCount >= this.totalCardsCount) {
        return
      }

      this.loadedCardsCount += cardsCount

      for (let i = 0; i < cardsCount; ++i) {
        this.leftColumnCards.push({
          imageSrc: require("@/assets/images/01.jpg"),
          number: this.leftColumnCards.length + this.rightColumnCards.length + 1
        })
      }
    }
  }
}
</script>

<style scoped lang="scss">
.task1 {
  margin: 20px auto 0 auto;
  padding: 0 15px;
  max-width: 1350px;

  &__content {
    display: flex;
  }

}
</style>
