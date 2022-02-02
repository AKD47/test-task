<template>
  <div class="base-wrapper">
    <base-header/>
    <div class="base-wrapper__content">
      <router-view/>
    </div>
  </div>
</template>

<script>
import BaseHeader from "@/components/baseWrapper/BaseHeader";

export default {
  name: 'base-wrapper',
  components: { BaseHeader }
}
</script>

<style lang="scss">
</style>
