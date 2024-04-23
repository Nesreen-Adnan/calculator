<template lang="pug">
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
  props: ["result"],
  data() {
    return {
      numbers: null,
    };
  },
  methods: {
    enter(e, operator) {
      let val = e.target.textContent,
        numbers = this.numbers,
        result = this.result;
      // to avoid repeat dot in the same num
      if (val != ".") {
        // to avoid start with operator
        if (!operator || (operator && numbers && !result[result.length - 1].match(/[-*+//]/))) 
          this.$emit("setResult", result + val);
      } else if (numbers[numbers.length - 1].indexOf(".") == -1 && result) 
        this.$emit("setResult", result + ".");
      this.numbers = result.split(/[-*+//]/);
    },
    calc() {
      let statement = this.result.replaceAll("x", "*");
      this.$emit("setResult", `${eval(statement)}`);
      let resultLength = this.result.toString().length;
      if (resultLength > 24) {
        this.$refs.screen.style.fontSize = "20px";
      } else if (resultLength > 15) {
        this.$refs.screen.style.fontSize = "28px";
      }
    },
    reset() {
      this.$emit("setResult", "");
      this.$refs.screen.style.fontSize = "38px";
    },
    del() {
      let result = this.result;
      if (result)
        this.$emit("setResult", result.substring(0, result.length - 1));
    },
  },
};
</script>

<style lang="scss">
.keyboard {
    display: grid;
    padding: 20px;
    grid-template-columns: repeat(4, 1fr);
    gap: 20px;
    background-color: var(--mainColor);
    border-radius: var(--radius);
    transition: var(--transition2);
    > * {
    display: flex;
    justify-content: center;
    align-items: center;
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
