<template>
  <div v-if="cardData" class="card">
    <img :src="cardData.imageSrc" alt="">
    <span>{{ cardData.number }}</span>
  </div>
</template>

<script>
export default {
  name: "v-card",
  props: {
    cardData: {type: Object}
  },
  methods: {

  }
}
</script>


<style scoped lang="scss">
.card {
  //border-radius: 8px;

  img {
    object-fit: cover;
    width: 100%;
    height: 100px;

    //border: 1px solid transparent;
    border-radius: 8px;

    transition: 200ms;
    //&:hover {
    //  //border-color: #409eff;
    //  box-shadow: 0 0 8px 0 rgb(232 237 250 / 60%), 0 2px 4px 0 rgb(232 237 250 / 50%);
    //}
  }
  span {
    position: absolute;
    top: -7px;
    right: 0;

    padding: 1px 3px;

    display: flex;
    justify-content: center;
    align-items: center;
    height: 20px;
    min-width: 20px;

    font-size: 12px;
    color: #FFFFFF;

    background-color: #202020;
    border-radius: 50%;
  }
}
</style>
