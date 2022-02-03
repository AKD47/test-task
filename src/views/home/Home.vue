<template>
  <div class="home">
    <div class="home__content">
      <task-card :image="require('@/assets/images/number-one.png')"
                 title="Задача 1"
                 description="Контейнеры, infinite scroll, tooltip, перенос карточки по клику"
                 route="/task1"/>
      <task-card :image="require('@/assets/images/number-2.png')"
                 title="Задача 2"
                 description="Круговой прогресс с различными параметрами"
                 route="/task2"/>
    </div>
  </div>
</template>

<script>
import TaskCard from "@/views/home/TaskCard";

export default {
  name: 'home',
  components: { TaskCard }
}
</script>

<style scoped lang="scss">
.home {
  display: flex;
  justify-content: center;
  align-items: center;

  width: 100%;
  height: calc(100vh - 70px);

  &__content {
    display: flex;
  }

}
</style>
