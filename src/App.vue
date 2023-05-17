<script setup lang="ts">
import CustomButton from './components/UI/CustomButton.vue'

</script>

<template>
    <div class="container">
        <div class="buttons-wrapper">
            <CustomButton :type="'Clear'" :text="'Отправить сообщение'"/>
            <CustomButton :type="'Primary'" :text="'Отправить сообщение'"/>
            <CustomButton :type="'Primary'" :text="'Отправить сообщение'" :timer="true" :duration="10" :waitText="'Отправить повторно'"/>
            <CustomButton :type="'Primary'" :text="'Отправить сообщение'" :icon="'rightArrow'" :iconPosition="'Right'"/>
            <CustomButton :type="'Primary'" :text="'Отправить сообщение'" :icon="'rightArrow'" :iconPosition="'Right'" :disabled="true"/>
            <CustomButton :type="'Primary'" :text="'Отправить сообщение'" :icon="'leftArrow'" :iconPosition="'Left'"/>
            <CustomButton :type="'Primary'" :text="'Отправить сообщение'" :icon="'leftArrow'" :iconPosition="'Left'"  :disabled="true"/>
            <CustomButton :type="'Primary'" :text="'Отправить сообщение'" :icon="'close'" :disabled="true" :iconPosition="'Right'"/>
            <CustomButton :type="'Icon'" :icon="'heart'" :size="'sm'"/>
            <CustomButton :type="'Icon'" :icon="'close'"/>
            <CustomButton :type="'Icon'" :icon="'rightArrow'"/>
            <CustomButton :type="'Icon'" :icon="'heart'" :disabled="true"/>

        </div>
    </div>
</template>

<style scoped>
.buttons-wrapper{
    display: grid;
    grid-auto-flow: column;
    grid-template-rows: repeat(4,auto);
    row-gap: 20px;
    column-gap: 10px;
    align-items: center;
}
</style>
