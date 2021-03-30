<template>
  <div class="calculator-wrapper">
    <h1 class="calculator-wrapper__heading">Cabinet Door Calculator</h1>
    <div class="calculator-wrapper__left">

    </div>
    <div class="calculator-wrapper__right">

    </div>
  </div>
</template>

<script>
import Logo from '~/components/Logo.vue'
import VuetifyLogo from '~/components/VuetifyLogo.vue'

export default {
  components: {
    Logo,
    VuetifyLogo
  }
}
</script>
<style lang="scss">
.calculator-wrapper {
  background:#f3eded;
  max-width:800px;
  width:100%;
  display:grid;
  grid-template-areas:"heading heading"
    "left right";
  padding:20px 45px;
  margin:auto;
  &__left {
    grid-area:left;
  }
  &__right {
    grid-area:right;
  }
  &__heading {
    color:black;
  }
}
</style>