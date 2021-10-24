<template>
  <div class="calculator">
    <table class="calculator__table" cellspacing="10">
      <tr>
        <td colspan="4">
          <input class="calculator__table--input" type="text" disabled />
        </td>
      </tr>
      <tr>
        <td class="calculator__button top">C</td>
        <td class="calculator__button top">+/-</td>
        <td class="calculator__button top">%</td>
        <td class="calculator__button right">/</td>
      </tr>
      <tr>
        <td class="calculator__button common">7</td>
        <td class="calculator__button common">8</td>
        <td class="calculator__button common">9</td>
        <td class="calculator__button right">*</td>
      </tr>
      <tr>
        <td class="calculator__button common">4</td>
        <td class="calculator__button common">5</td>
        <td class="calculator__button common">6</td>
        <td class="calculator__button right">-</td>
      </tr>
      <tr>
        <td class="calculator__button common">1</td>
        <td class="calculator__button common">2</td>
        <td class="calculator__button common">3</td>
        <td class="calculator__button right">+</td>
      </tr>
      <tr>
        <td class="calculator__button--colspan-2 common" colspan="2">0</td>
        <td class="calculator__button common">.</td>
        <td class="calculator__button right">=</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  setup() {
    return {};
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
    width: 30rem;
    &--input {
      display: block;
      height: 7.5rem;
      padding: 0.5rem 2rem;
      margin-bottom: 1rem;
      border: none;
      font-size: 4rem;
      background: $background-color;
      color: $main-color;
      text-align: right;
    }
  }
  &__button {
    margin: 1rem;
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
