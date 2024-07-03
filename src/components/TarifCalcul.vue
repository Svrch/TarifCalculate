<template>
  <div>
    <TitleCalcul>Тарифный калькулятор</TitleCalcul>
    <div class="Tarif-calcul">
      <div class="Tarif-calcul__options">
        <PayPeriod v-model:tab="tabSelected"></PayPeriod>
        <PayCurrency v-model:tab="currencySelected"></PayCurrency>
      </div>
      <div class="Tarif-calcul__tabs">
        <TarifTab>
          <template #label>
            Стандарт
          </template>
          <template #info>
            <ul>
              <li>Инфо 1</li>
              <li>Инфо 2</li>
            </ul>
          </template>
          <template #btn>
            {{ priceStandart }}
          </template>
          <template #sale>
            <div v-if="tabSelected !== 'mounth'">{{ standartEconomy }} <br /> при оплате за год</div>
          </template>
        </TarifTab>
        <TarifTab>
          <template #label>
            Продвинутый
          </template>
          <template #info>
            <ul>
              <li>Инфо 1</li>
              <li>Инфо 2</li>
            </ul>
          </template>
          <template #btn>
            {{ pricePro }}
          </template>
          <template #sale>
            <div v-if="tabSelected !== 'mounth'">{{ proEconomy }} <br /> при оплате за год</div>
          </template>
        </TarifTab>
      </div>
    </div>
  </div>
</template>

<script setup>
import PayCurrency from "./TarifCalcul/PayCurrency.vue";
import TitleCalcul from "./TarifCalcul/TitleCalcul.vue";
import PayPeriod from "./TarifCalcul/PayPeriod.vue";
import TarifTab from "./TarifCalcul/TarifTab.vue";
import { computed, onMounted, ref } from 'vue'

const tabSelected = ref('mounth')
const currencySelected = ref('RUB')
const currencyValues = ref({ RUB: 0, CNY: 0, KZT: 0 })

const price = ref({
  Standart: { mounth: 100, year: 1000 },
  Pro: { mounth: 150, year: 1400 },
  Currency: currencySelected
})

const apiKey = '5ec993e59961441f87c8ce390982cfc8'

const currency = async () => {
  const res = await fetch(`https://api.currencyfreaks.com/v2.0/rates/latest?apikey=${apiKey}`)
  const data = await res.json()
  for (let item in currencyValues.value) {
    currencyValues.value[item] = Number(data.rates[item])
  }
  return data.rates
}

onMounted(() => {
  currency()
})

const priceStandart = computed(() => {
  const currPrice = ((tabSelected.value === 'mounth' ? price.value.Standart.mounth : price.value.Standart.year) / currencyValues.value.RUB * currencyValues.value[currencySelected.value]).toFixed(2)
  return currPrice + ' ' + currencySelected.value + '/' + tabSelected.value
})

const pricePro = computed(() => {
  const currPrice = ((tabSelected.value === 'mounth' ? price.value.Pro.mounth : price.value.Pro.year) / currencyValues.value.RUB * currencyValues.value[currencySelected.value]).toFixed(2)
  return currPrice + ' ' + currencySelected.value + '/' + tabSelected.value
})

const standartEconomy = computed(() => {
  const economy = 'Экономия ' + ((price.value.Standart.mounth / currencyValues.value.RUB * currencyValues.value[currencySelected.value] * 12) - price.value.Standart.year / currencyValues.value.RUB * currencyValues.value[currencySelected.value]).toFixed(2) + ' ' + currencySelected.value
  return economy
})

const proEconomy = computed(() => {
  const economy = 'Экономия ' + ((price.value.Pro.mounth / currencyValues.value.RUB * currencyValues.value[currencySelected.value] * 12) - price.value.Pro.year / currencyValues.value.RUB * currencyValues.value[currencySelected.value]).toFixed(2) + ' ' + currencySelected.value
  return economy
})
</script>

<style lang="scss" scoped>
.Tarif-calcul {
  &__options {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    gap: 10px;
  }

  &__tabs {
    margin-top: 36px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    gap: 30px;
  }
}

@media (min-width:800px) {
  .Tarif-calcul {
    &__options {
      display: flex;
      flex-direction: row;
      justify-content: center;
      gap: 30px;
    }
  }
}
</style>
