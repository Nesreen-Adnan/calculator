<template lang="pug">
.container 
  Header
  Screen(:result="result")
  Keyboard(:result="result" @setResult="setResult")
</template>

<script>
import {Header, Screen, Keyboard} from "./components/index.js";
export default {
  data() {
    return {
      result: "",
    };
  },
  methods: {
    setResult(val) {
      this.result = val;
    },
  },
  components: {
    Header, 
    Screen, 
    Keyboard
  }
};
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=League+Spartan:wght@700&display=swap");
:root {
  --bodyBg: hsl(222, 26%, 31%);
  --mainColor: hsl(223, 31%, 20%);
  --screenBg: hsl(224, 36%, 15%);
  --secondColor: hsl(6, 63%, 50%);
  --secondLightColor: hsl(9, 93%, 67%);
  --secondShadowColor: hsl(6, 70%, 34%);
  --keyBg: hsl(30, 25%, 89%);
  --keyLightBg: hsl(0, 0%, 100%);
  --keyShadow: hsl(28, 16%, 65%);
  --specialKeyBg: hsl(225, 21%, 49%);
  --specialKeyLightBg: hsl(224, 51%, 76%);
  --specialKeyShadow: hsl(224, 28%, 35%);
  --textColor: hsl(221, 14%, 31%);
  --radius: 8px;
  --equalKeyColor: #fff;
  --transition: 0.17s;
  --transition2: .7s;
}
body {
  font-family: "League Spartan", sans-serif;
  font-weight: 700;
  color: #fff;
  background-color: var(--bodyBg);
  transition: var(--transition2);
}
//start global
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
.up {
  text-transform: uppercase;
}
.normal {
  text-transform: none;
}
@mixin flex($justify: center, $align: center, $gap: 10px) {
  display: flex;
  justify-content: $justify;
  align-items: $align;
  gap: $gap;
}
.flex {
  @include flex();
}
//end global
#app {
  position: relative;
  @include flex();
  height: 100vh;
}
.container {
  position: absolute;
  left: 50%;
  top: 50%;
  width: 80%;
  max-width: 450px;
  transform: translate(-50%, -50%)
}
</style>
