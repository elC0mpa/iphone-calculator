<template>
  <div class="calculator">
    <table class="calculator__table" cellspacing="10">
      <tr>
        <td colspan="4">
          <input
            v-model="actualValue"
            class="calculator__table--input"
            type="text"
            disabled
          />
        </td>
      </tr>
      <tr>
        <td class="calculator__button top" @click="clear">C</td>
        <td class="calculator__button top" @click="invert">+/-</td>
        <td class="calculator__button top" @click="percent">%</td>
        <td class="calculator__button right" @click="operator">/</td>
      </tr>
      <tr>
        <td class="calculator__button common" @click="concat">7</td>
        <td class="calculator__button common" @click="concat">8</td>
        <td class="calculator__button common" @click="concat">9</td>
        <td class="calculator__button right" @click="operator">*</td>
      </tr>
      <tr>
        <td class="calculator__button common" @click="concat">4</td>
        <td class="calculator__button common" @click="concat">5</td>
        <td class="calculator__button common" @click="concat">6</td>
        <td class="calculator__button right" @click="operator">-</td>
      </tr>
      <tr>
        <td class="calculator__button common" @click="concat">1</td>
        <td class="calculator__button common" @click="concat">2</td>
        <td class="calculator__button common" @click="concat">3</td>
        <td class="calculator__button right" @click="operator">+</td>
      </tr>
      <tr>
        <td
          class="calculator__button--colspan-2 common"
          colspan="2"
          @click="concat"
        >
          0
        </td>
        <td class="calculator__button common" @click="addPoint">.</td>
        <td class="calculator__button right" @click="equal">=</td>
      </tr>
    </table>
  </div>
</template>

<script>
import { reactive, toRefs } from "@vue/reactivity";
export default {
  setup() {
    const state = reactive({
      actualValue: 0,
      previousValue: 0,
      operator: undefined,
      reset: false,
    });
    const concat = (e) => {
      if (state.reset) {
        state.reset = false;
        state.actualValue = 0;
      }
      const number = e.target.innerText;
      const temp = state.actualValue.toString() + number.toString();
      state.actualValue = Number(temp);
    };
    const clear = () => {
      state.actualValue = 0;
      state.previousValue = 0;
      state.operator = undefined;
    };
    const invert = () => {
      state.actualValue = state.actualValue * -1;
    };
    const percent = () => {
      state.actualValue = state.actualValue / 100;
    };
    const addPoint = () => {
      if (!state.actualValue.toString().includes(".")) {
        state.actualValue = state.actualValue.toString() + ".";
      }
    };
    const getResult = () => {
      console.log(state.actualValue, state.operator, state.previousValue);
      let value = 0;
      switch (state.operator) {
        case "+":
          value = Number(state.actualValue) + Number(state.previousValue);
          break;
        case "-":
          value = Number(state.previousValue) - Number(state.actualValue);
          break;
        case "*":
          value = Number(state.actualValue) * Number(state.previousValue);
          break;
        case "/":
          value = Number(state.previousValue) / Number(state.actualValue);
          break;
      }
      state.actualValue = value;
    };
    const operator = (e) => {
      if (state.previousValue !== 0) {
        getResult();
      }
      state.previousValue = state.actualValue;
      state.operator = e.target.innerText;
      state.reset = true;
    };
    const equal = () => {
      getResult();
      state.previousValue = 0;
      state.operator = undefined;
      state.reset = true;
    };

    return {
      concat,
      ...toRefs(state),
      clear,
      invert,
      percent,
      addPoint,
      operator,
      equal,
    };
  },
};
</script>

<style lang="scss">
.calculator {
  width: 100vw;
  height: 100vh;
  background: $background-color;
  display: flex;
  justify-content: center;
  align-items: center;
  font-size: 3rem;
  &__table {
    color: $main-color;
    &--input {
      display: block;
      border: none;
      padding: 0.5rem 2rem;
      font-size: 4rem;
      background: transparentize($background-color, 0.8);
      color: $main-color;
      text-align: right;
    }
  }
  &__button {
    border-radius: 4rem;
    width: 8rem;
    height: 8rem;
    text-align: center;
    font-weight: bold;
    cursor: pointer;
    &--colspan-2 {
      border-radius: 4rem;
      width: 16rem;
      height: 8rem;
      text-align: center;
      font-weight: bold;
      cursor: pointer;
    }
  }
  .common {
    background: $common-button-background;
    color: $background-color;
    &:hover {
      background: $common-button-background-hover;
    }
  }
  .right {
    background: $right-column-button-background;
    color: $main-color;
    &:hover {
      background: $right-column-button-background-hover;
    }
  }
  .top {
    background: $top-row-button-background;
    color: $main-color;
    &:hover {
      background: $top-row-button-background-hover;
    }
  }
}
</style>
