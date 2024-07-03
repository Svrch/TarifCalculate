<template>
  <div class="Pay-period">
    <div class="Pay-period__label">
      Период
    </div>
    <div class="Pay-period__tabs">
      <div
        @click="clickOnTab('mounth')"
        :class="['Pay-period__tabs-mounth', { 'selected': tab === 'mounth' }]"
      >
        На месяц
      </div>
      <div
        @click="clickOnTab('year')"
        :class="['Pay-period__tabs-year', { 'selected': tab === 'year' }]"
      >
        На год
        <span class="Pay-period__tabs-year-sale">Выгодно</span>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits('update:tab')

const clickOnTab = (tabName) => {
  emit('update:tab', tabName)
}

const props = defineProps({
  tab: {
    type: String,
    required: false,
    default: 'mounth'
  }
})
</script>

<style lang="scss" scoped>
.selected {
  background-color: #3694ff;

  .Pay-period__tabs-year-sale {
    color: #fbfbfb;
  }
}

.Pay-period {
  font-size: 24px;
  color: #fbfbfb;
  font-family: "Gilroy-light", Arial, sans-serif;

  &__label {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 48px;
  }

  &__tabs {
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: #333333;
    border: solid 2px #3694ff;
    width: 350px;
    cursor: pointer;

    &-mounth {
      padding-left: 12px;
      padding-right: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 48px;
      width: 50%;

      &:hover {
        background-color: #3694ff;
      }
    }

    &-year {
      padding-left: 12px;
      padding-right: 12px;
      display: flex;
      align-items: center;
      justify-content: center;
      height: 48px;
      width: 50%;

      &:hover {
        background-color: #3694ff;

        .Pay-period__tabs-year-sale {
          color: #fbfbfb;
        }
      }

      &-sale {
        color: #3694ff;
        font-size: 15px;
        padding-left: 12px;
      }
    }
  }
}
</style>
