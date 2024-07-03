<template>
    <div class="Tarif-tab">
        <div class="Tarif-tab__label">
            <slot name="label" />
        </div>
        <div class="Tarif-tab__info">
            <slot name="info" />
        </div>
        <div class="Tarif-tab__btn">
            <slot name="btn" />
        </div>
        <div class="Tarif-tab__sale">
            <slot name="sale" />
        </div>
    </div>
</template>

<script setup></script>

<style lang="scss" scoped>
.Tarif-tab {
    font-size: 24px;
    color: #fbfbfb;
    font-family: "Gilroy-light", Arial, sans-serif;
    background-color: #333333;
    width: 530px;

    &__label {
        display: flex;
        justify-content: center;
        font-family: "Gilroy-bold", Arial, sans-serif;
        font-size: 36px;
        margin: 24px 0px;
    }

    &__info {
        margin: 24px 50px;
    }

    &__btn {
        display: flex;
        justify-content: center;
        align-items: center;
        margin-top: 24px;
        margin-bottom: 24px;
        margin-left: auto;
        margin-right: auto;
        border: solid 1px #3694ff;
        max-width: 300px;
        height: 62px;
        cursor: pointer;

        &:hover {
            background-color: #3694ff;
        }
    }

    &__sale {
        display: flex;
        justify-content: center;
        align-items: center;
        margin: 24px 50px;
        font-size: 20px;
    }
}
</style>