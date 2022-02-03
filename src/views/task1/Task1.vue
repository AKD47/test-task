<template>
  <div class="task1">
    <div class="task1__content">
      <list :list="leftColumnCards"
            @got-to-bottom="loadCards(20)"
            @move-card="moveToRight"/>
      <list :list="rightColumnCards"
            @move-card="moveToLeft"/>
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
    moveToRight(index) {
      const card = this.leftColumnCards[index]
      this.leftColumnCards.splice(index, 1)
      this.rightColumnCards.push(card)
    },
    moveToLeft(index) {
      const card = this.rightColumnCards[index]
      this.rightColumnCards.splice(index, 1)
      this.leftColumnCards.push(card)
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

    },
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
