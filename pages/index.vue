<template>
  <div class="calculator-wrapper">
    <h1 class="calculator-wrapper__heading">Cabinet Door Calculator</h1>
    <div class="calculator-wrapper__left">
      <label for="width">Width (inches)</label>
      <input id="width" type="number" class="calculator-wrapper__input calc-input" />
      <label for="height">Height (inches)</label>
      <input id="height" type="number" class="calculator-wrapper__input calc-input" />
      <label for="reveal">Reveal</label>
      <div class="slidecontainer">
        <div id="revealresult"></div>
        <input type="range" min="0" max="2" value=".125" class="slider calc-input" id="revealslide" step=".125">
      </div>
      <label for="overlay">Overlay</label>
      <div class="slidecontainer">
        <div id="overlayresult"></div>
        <input type="range" min="0" max="4" value=".5" class="slider calc-input" id="overlayslide" step=".5">
      </div>
    </div>
    <div class="calculator-wrapper__right">
      <h2 class="content-heading">Double Door</h2>
      <div class="results">
        <div class="results__group">
          <label class="text--large">Inset: </label>
          <div id="double_inset_result"></div>
        </div>
        <div class="results__group">
          <label class="text--large">Overlay: </label>
          <div id="double_overlay_result"></div>
        </div>
      </div>
      <h2 class="content-heading">Single Door</h2>
      <div class="results">
        <div class="results__group">
          <label class="text--large">Inset: </label>
          <div id="single_inset_result"></div>
        </div>
        <div class="results__group">
          <label class="text--large">Overlay: </label>
          <div id="single_overlay_result"></div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    document.getElementById("revealresult").innerHTML = .125
    document.getElementById("overlayresult").innerHTML = .5
    
    
    const revealslide = document.querySelector("#revealslide");
    const overlayslide = document.querySelector("#overlayslide")
    const overlayresult = document.querySelector("#overlayresult")
    const revealresult = document.querySelector("#revealresult");
    const inputs = document.querySelectorAll('.calc-input');
    const doubleinsetfinal = document.getElementById("double_inset_result")
    const doubleoverlayfinal = document.getElementById("double_overlay_result")
    const singleoverlayfinal = document.getElementById("single_overlay_result")
    const singleinsetfinal = document.getElementById("single_inset_result")
    
    revealslide.addEventListener('input', (event) => {
      revealresult.textContent = event.target.value
    })
    overlayslide.addEventListener('input', (event) => {
      overlayresult.textContent = event.target.value
    })
    inputs.forEach((input) => {
      input.addEventListener('input', (event) => {
        var width = parseInt(document.getElementById("width").value, 10);
        var height = parseInt(document.getElementById("height").value, 10);
        var reveal = revealresult.textContent
        var overlay = overlayresult.textContent
        var insetresult = doubleDoorLogic(width, height, reveal, overlay, "inset")
        var overlayFinal = doubleDoorLogic(width, height, reveal, overlay, "overlay")
        var singleOverlayFinal = singleDoorLogic(width, height, reveal, overlay, "overlay")
        var singleInsetFinal = singleDoorLogic(width, height, reveal, overlay, "inset")

        doubleinsetfinal.textContent = insetresult
        doubleoverlayfinal.textContent = overlayFinal
        singleoverlayfinal.textContent = singleOverlayFinal
        singleinsetfinal.textContent = singleInsetFinal
      })
    })

    function doubleDoorLogic(width, height, reveal, overlay, type) {
      var rWidth = ""
      var rHeight = ""
      switch (type) {
        case "inset":
          rWidth = ((width - (2 * reveal)) * .5) - reveal * .5
          rHeight = height - (reveal*2)
          break;
        case "overlay":
          rWidth = ((width + (2*overlay)) * .5) - reveal * .5
          rHeight = height + (overlay*2)
      }
      return `The door to order is ${rWidth}'' x ${rHeight}''`
    }
    function singleDoorLogic(width, height, reveal, overlay, type) {
      var rWidth = ""
      var rHeight = ""
      switch (type) {
        case "overlay":
          rWidth = width + (overlay*2)
          rHeight = height + (overlay*2)
          break;
        case "inset":
          rWidth = width - (reveal*2)
          rHeight = height - (reveal*2)
      }
      return `The door to order is ${rWidth}'' x ${rHeight}''`
    }
  }
}
</script>
<style lang="scss">
input[type=range] {
  height: 38px;
  -webkit-appearance: none;
  margin: 10px 0;
  width: 100%;
}
input[type=range]:focus {
  outline: none;
}
input[type=range]::-webkit-slider-runnable-track {
  width: 100%;
  height: 10px;
  cursor: pointer;
  animate: 0.2s;
  box-shadow: 1px 1px 1px #000000;
  background: #3071A9;
  border-radius: 5px;
  border: 1px solid #000000;
}
input[type=range]::-webkit-slider-thumb {
  box-shadow: 1px 1px 1px #000000;
  border: 1px solid #000000;
  height: 30px;
  width: 15px;
  border-radius: 5px;
  background: #FFFFFF;
  cursor: pointer;
  -webkit-appearance: none;
  margin-top: -11px;
}
input[type=range]:focus::-webkit-slider-runnable-track {
  background: #3071A9;
}
.content-heading {
  margin-bottom:20px;
}
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
  row-gap:20px;
  grid-template-columns:1fr 1fr;
  label {
    color:black;
  }
  &__left {
    grid-area:left;
    width:100%;
    flex-direction:column;
    display:flex;
    max-width:310px;
  }
  &__right {
    grid-area:right;
    display:grid;
    grid-template-rows:50px 1fr 50px 1fr;
  }
  &__heading {
    color:black;
    grid-area:heading;
    text-align:center;
  }
  &__input {
    padding:6px 12px;
    border:1px solid black;
    border-radius:10px;
    margin-bottom:10px;
  }
}
.results {
  display:flex;
  flex-direction: column;
  &__group {
    label {
      font-weight:bold;
      font-size:18px;
      margin-right:10px;
    }
    &:not(:last-child) {
      padding-bottom:10px;
    }
    display:inline-flex;
    align-items:center;
  }
}
</style>