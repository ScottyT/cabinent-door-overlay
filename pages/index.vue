<template>
  <div class="calculator-wrapper">
    <h1 class="calculator-wrapper__heading">Cabinet Door Calculator</h1>
    <div class="calculator-wrapper__left">
      <label for="width">Width (inches)</label>
      <input id="width" type="number" class="calculator-wrapper__input" @input="calculate" />
      <label for="height">Height (inches)</label>
      <input id="height" type="number" class="calculator-wrapper__input" @input="calculate" />
      <label for="reveal">Reveal</label>
      <input id="reveal" type="number" class="calculator-wrapper__input result" @input="calculate" />
      <label for="overlay">Overlay</label>
      <input id="overlay" type="number" class="calculator-wrapper__input result" @input="calculate" />
    </div>
    <div class="calculator-wrapper__right">
      <h3>Inset</h3>
      <div id="inset_result"></div>
      <h3>Overlay</h3>
      <div id="overlay_result"></div>
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
  },
  data() {
    return {
      width:null,
      height:null,
      overlay: null,
      reveal: null
    }
  },
  computed: {

  },
  mounted() {
    document.getElementById("reveal").value = .125
    document.getElementById("overlay").value = .5
  },
  methods: {
    calculate() {
      var width = parseInt(document.getElementById("width").value, 10);
      var height = document.getElementById("height").value;
      var reveal = document.getElementById("reveal").value;
      var overlay = document.getElementById("overlay").value;
      
      var insetresult = ((width - (2*reveal)) * .5) - reveal *.5
      var overlayresult = ((width + (2*overlay)) * .5) - reveal * .5
      if (isNaN(insetresult) || isNaN(overlayresult)) {
        insetresult = 0
        overlayresult = 0       
      }
      
      document.getElementById("inset_result").innerHTML = insetresult + " inches"
      document.getElementById("overlay_result").innerHTML = overlayresult + " inches"
      
    },
    setValues() {
      document.getElementById("reveal").value = .125
    }
  },
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
  color:black;
  label {
    color:black;
  }
  &__left {
    grid-area:left;
    width:50%;
    flex-direction:column;
    display:flex;
  }
  &__right {
    grid-area:right;
  }
  &__heading {
    color:black;
  }
  &__input {
    padding:6px 12px;
    border:1px solid black;
    border-radius:10px;
    margin-bottom:10px;
  }
}
</style>