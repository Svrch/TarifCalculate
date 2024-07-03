<template>
  <div class="Pay-currency">
    <div class="Pay-currency__label">
      Валюта
    </div>
    <div class="Pay-currency__select">
      <select @input="handeClick($event)">
        <option selected value="RUB">RUB</option>
        <option value="CNY"><img src="">CNY</option>
        <option value="KZT">KZT</option>
      </select>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits('update:tab')

const handeClick = (event) => {
  emit('update:tab', event.target.value)
}
</script>

<style lang="scss" scoped>
.Pay-currency {
  font-size: 24px;
  color: #fbfbfb;
  font-family: "Gilroy-light", Arial, sans-serif;

  &__label {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 48px;
  }

  &__select {
    select {
      padding-right: 48px;
      padding-left: 12px;
      appearance: none;
      border: 0;
      outline: 0;
      background: var(--arrow-icon) no-repeat right center #333333;
      font-size: 24px;
      color: #fbfbfb;
      font-family: "Gilroy-light", Arial, sans-serif;
      height: 48px;
      cursor: pointer;
      border: solid 2px #333333;
    }

    option {
      background-image: var(--arrow-icon);
    }
  }
}
</style>
