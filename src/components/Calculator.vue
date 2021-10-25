<template>
  <div class="calculator">
    <div class="calculator__row">
      <input
        v-model="actualValue"
        class="calculator__input col-span-4"
        type="text"
        disabled
      />
    </div>
    <div class="calculator__row">
      <button class="calculator__button top" @click="clear">C</button>
      <button class="calculator__button top" @click="invert">+/-</button>
      <button class="calculator__button top" @click="percent">%</button>
      <button class="calculator__button right" @click="operator">/</button>
    </div>
    <div class="calculator__row">
      <button class="calculator__button common" @click="concat">7</button>
      <button class="calculator__button common" @click="concat">8</button>
      <button class="calculator__button common" @click="concat">9</button>
      <button class="calculator__button right" @click="operator">*</button>
    </div>
    <div class="calculator__row">
      <button class="calculator__button common" @click="concat">4</button>
      <button class="calculator__button common" @click="concat">5</button>
      <button class="calculator__button common" @click="concat">6</button>
      <button class="calculator__button right" @click="operator">-</button>
    </div>
    <div class="calculator__row">
      <button class="calculator__button common" @click="concat">1</button>
      <button class="calculator__button common" @click="concat">2</button>
      <button class="calculator__button common" @click="concat">3</button>
      <button class="calculator__button right" @click="operator">+</button>
    </div>
    <div class="calculator__row">
      <button class="calculator__button col-span-2 common" @click="concat">
        0
      </button>
      <button class="calculator__button common" @click="addPoint">.</button>
      <button class="calculator__button right" @click="equal">=</button>
    </div>
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
  width: 35rem;
  @include responsive(smallest-bp) {
    width: 30rem;
  }
  &__row {
    margin-bottom: 0.5rem;
    display: flex;
    > * {
      flex: 0 0 25%;
    }
    > .col-span-4 {
      flex: 0 0 100%;
    }
    > .col-span-2 {
      flex: 0 0 50%;
    }
  }
  &__input {
    width: 100%;
    border: none;
    padding: 0.5rem 2rem;
    font-size: 4rem;
    background: transparent;
    color: $main-color;
    text-align: right;
  }
  &__button {
    font-size: 2rem;
    border-radius: 3rem;
    height: 6rem;
    text-align: center;
    font-weight: bold;
    cursor: pointer;
    margin-right: 0.5rem;
    border: none;
    &.col-span-2 {
      margin-right: 1rem;
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
