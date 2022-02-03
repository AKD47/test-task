<template>
  <div class="task2">
    <div class="task2__progress-wrapper">
      <arc-progress-bar
          :progress="progress"
          :diameter="diameter"
          :bg-color="bgColor"
          :line-color="lineColor"
          :weight="weight"
          :visible-part-of-circle="visiblePartOfCircle"
          :max-progress="maxProgress"
          :counter-position="counterPosition"/>
    </div>
    <div class="task2__actions">

      <base-input-number v-model="progress"
                         label="Значение прогресса (0-100%)"
                         :step="5"
                         :min="0" :max="100"/>

      <base-input-number v-model="diameter"
                         label="Диаметр (50-400px)"
                         :step="10"
                         :min="50" :max="400"/>

      <base-input-number v-model="weight"
                         label="Ширина линии (1-7)"
                         :step="0.5"
                         :min="1" :max="7"/>

      <base-input v-model="bgColor"
                  label="Цвет фоновой линии"/>

      <base-input v-model="lineColor"
                  label="Цвет линии прогресса"/>


      <base-input-number v-model="visiblePartOfCircle"
                         label="Видимая часть окружности (30-100%)"
                         :step="5"
                         :min="30" :max="100"/>

      <base-input-number v-model="maxProgress"
                         label="Макс. значение прогресса (0-100%)"
                         :step="5"
                         :min="0" :max="100"/>

      <div style="text-align: left">
        <label>Позиция счетчика</label>
        <div>
          <label>
            <span>Center</span>
            <input v-model="counterPosition" type="radio" value="center">
          </label>
        </div>
        <div>
          <label>
            <span>Bottom</span>
            <input v-model="counterPosition" type="radio" value="bottom">
          </label>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
import ArcProgressBar from "@/components/ArcProgressBar";
import BaseInput from "@/components/BaseInput";
import BaseInputNumber from "@/components/BaseInputNumber";

export default {
  name: 'app',
  components: { ArcProgressBar, BaseInput, BaseInputNumber },
  data() {
    return {
      diameter: 300,
      progress: 70,
      weight: 5,
      bgColor: '#e5e9f2',
      lineColor: '#f56c6c',
      visiblePartOfCircle: 70,
      maxProgress: 100,
      // animate default linear // 9.
      // animateSpeed // 10.
      // отображать progress // 11.
      counterPosition: 'center' // 12.
    }
  }
}
</script>

<style scoped lang="scss">
.task2 {
  display: flex;

  &__progress-wrapper {
    display: flex;
    justify-content: center;
    align-items: center;

    width: 50%;
  }

  &__actions {
    width: 50%;
  }

}
</style>
