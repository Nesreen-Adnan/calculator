<template lang="pug">
.container 
  header
    .title calc
    .themes.flex
      span.up theme
      .choices
        - var themesNum = 3;
        .nums 
          - for (var i = 1; i <= themesNum; i++) 
            span= i
        .toggle 
          input(type="range", v-model="theme", min="1", max=themesNum, @input="changeTheme")
  .screen(v-text="result", ref="screen")
  .keyboard.up
    div(@click="enter") 7
    div(@click="enter") 8
    div(@click="enter") 9
    .del(@click="del") del
    div(@click="enter") 4
    div(@click="enter") 5
    div(@click="enter") 6
    .plus(@click="enter($event, '+')") +
    div(@click="enter") 1
    div(@click="enter") 2
    div(@click="enter") 3
    .sub(@click="enter($event, '-')") -
    .dot(@click="enter") .
    div(@click="enter") 0
    .division(@click="enter($event, '/')") /
    .mult.normal(@click="enter($event, '*')") x
    .reset(@click="reset") reset
    .equal(@click="calc") =
</template>

<script>
export default {
  data() {
    return {
      theme: 1,
      result: "",
      numbers: null,
      themes: [
        {
          "--bodyBg": 'hsl(222, 26%, 31%)',
          "--mainColor": 'hsl(223, 31%, 20%)',
          "--screenBg": 'hsl(224, 36%, 15%)',
          "--secondColor": 'hsl(6, 63%, 50%)',
          "--secondLightColor": 'hsl(9, 93%, 67%)',
          "--secondShadowColor": 'hsl(6, 70%, 34%)',
          "--keyBg": 'hsl(30, 25%, 89%)',
          "--keyLightBg": 'hsl(0, 0%, 100%)',
          "--keyShadow": 'hsl(28, 16%, 65%)',
          "--specialKeyBg": 'hsl(225, 21%, 49%)',
          "--specialKeyLightBg": 'hsl(224, 51%, 76%)',
          "--specialKeyShadow": 'hsl(224, 28%, 35%)',
          "--textColor": 'hsl(221, 14%, 31%)',
          "--textColor2": 'hsl(0, 0%, 100%)',
          "--equalKeyColor": '#fff',
        },
        {
          "--bodyBg": 'hsl(0, 0%, 90%)',
          "--mainColor": 'hsl(0, 5%, 81%)',
          "--screenBg": 'hsl(0, 0%, 93%)',
          "--secondColor": 'hsl(25, 98%, 40%)',
          "--secondLightColor": 'hsl(25, 100%, 61%)',
          "--secondShadowColor": 'hsl(25, 99%, 27%)',
          "--keyBg": 'hsl(45, 7%, 89%)',
          "--keyLightBg": 'hsl(0, 0%, 100%)',
          "--keyShadow": 'hsl(35, 11%, 61%)',
          "--specialKeyBg": 'hsl(185, 42%, 37%)',
          "--specialKeyLightBg": 'hsl(185, 41%, 56%)',
          "--specialKeyShadow": 'hsl(185, 58%, 25%)',
          "--textColor": 'hsl(60, 10%, 19%)',
          "--textColor2": 'hsl(60, 10%, 19%)',
          "--equalKeyColor": '#fff',
        },
        {
          "--bodyBg": 'hsl(268, 75%, 9%)',
          "--mainColor": 'hsl(268, 71%, 12%)',
          "--screenBg": 'hsl(268, 71%, 12%)',
          "--secondColor": 'hsl(176, 100%, 44%)',
          "--secondLightColor": 'hsl(177, 100%, 79%)',
          "--secondShadowColor": 'hsl(177, 92%, 70%)',
          "--keyBg": 'hsl(268, 47%, 21%)',
          "--keyLightBg": 'hsl(268, 54%, 44%)',
          "--keyShadow": 'hsl(290, 70%, 36%)',
          "--specialKeyBg": 'hsl(281, 89%, 26%)',
          "--specialKeyLightBg": 'hsl(280, 56%, 44%)',
          "--specialKeyShadow": 'hsl(285, 91%, 52%)',
          "--textColor": 'hsl(52, 100%, 62%)',
          "--textColor2": 'hsl(52, 100%, 62%)',
          "--equalKeyColor": 'hsl(198, 20%, 13%)',
        },
      ]
    };
  },
  methods: {
    enter(e, operator) {
      let val = e.target.textContent;
      // to avoid repeat dot in the same num
      if (val != ".") {
        // to avoid start with operator
        if (!operator || (operator && this.numbers[this.numbers.length - 1])) {
          this.result += val;
        }
      } else {
        if (this.numbers[this.numbers.length - 1].indexOf(".") == -1 && this.result) {
          this.result += ".";
        }
      }
      this.numbers = this.result.split(/[-*+//]/);
    },
    calc() {
      let statement = this.result.replaceAll("x", "*");
      this.result = eval(statement);
      let resultLength = this.result.toString().length;
      if (resultLength > 24) {
        this.$refs.screen.style.fontSize = "20px";
      } else if (resultLength > 15) {
        this.$refs.screen.style.fontSize = "28px";
      }
    },
    reset() {
      this.result = "";
      this.$refs.screen.style.fontSize = "38px";
    },
    del() {
      let result = this.result;
      if (result) {
        this.result = result.substring(0, result.length - 1);
      }
    },
    changeTheme() {
      let themeProperties = this.themes[this.theme - 1];
      for (let i = 0; i < Object.keys(themeProperties).length; i++) {
        let key = Object.keys(themeProperties)[i];
        console.log(key);
        document.documentElement.style.setProperty(key, themeProperties[key])
      }
    }
  },
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
  @include flex();
}
.container {
  width: 80%;
  max-width: 450px;
}
header {
  @include flex(space-between);
  margin: 25px 0;
  .title {
    font-size: 20px;
  }
  .themes {
    font-size: 10px;
    transition: var(--transition2);
    > span {
      margin-right: 15px;
    }
    .choices {
      .nums {
        padding: 0 7px;
        @include flex(space-between);
      }
      .toggle {
        padding: 2px;
        margin-top: 3px;
        background-color: var(--mainColor);
        border-radius: 25px;
        transition: var(--transition2);
        input {
          max-width: 60px;
          accent-color: var(--secondColor);
          appearance: none;
          background-color: transparent;
          cursor: pointer;
          transition: var(--transition);
          &:hover {
            accent-color: var(--secondLightColor);
          }
        }
      }
    }
  }
}
header .title, 
.screen, 
.themes {
  color: var(--textColor2);
}
.screen {
  @include flex(flex-end);
  padding: 10px;
  background-color: var(--screenBg);
  font-size: 38px;
  height: 90px;
  border-radius: var(--radius);
  margin-bottom: 20px;
  white-space: nowrap;
  overflow: hidden;
  transition: var(--transition2);
}
.keyboard {
  display: grid;
  padding: 20px;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
  background-color: var(--mainColor);
  border-radius: var(--radius);
  transition: var(--transition2);
  > * {
    @include flex();
    font-size: 25px;
    color: var(--textColor);
    cursor: pointer;
    background-color: var(--keyBg);
    box-shadow: 0 3px var(--keyShadow);
    border-radius: var(--radius);
    padding: 10px;
    transition: var(--transition);
    &:hover {
      background-color: var(--keyLightBg);
    }
    &.del,
    &.reset {
      font-size: 20px;
      color: #fff;
      background-color: var(--specialKeyBg);
      box-shadow: 0 3px var(--specialKeyShadow);
      &:hover {
        background-color: var(--specialKeyLightBg);
      }
    }
    &.reset {
      grid-column: 1 / 3;
    }
    &.equal {
      color: var(--equalKeyColor);
      background-color: var(--secondColor);
      box-shadow: 0 3px var(--secondShadowColor);
      grid-column: 3 / 5;
      &:hover {
        background-color: var(--secondLightColor);
      }
    }
  }
}
</style>
