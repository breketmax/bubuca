<script setup lang="ts">
import {defineProps, onMounted, onUnmounted, ref} from "vue";

interface ITimer{
    duration:number
}

const props =defineProps<ITimer>()
const emit = defineEmits(['endTimer'])
const duration =ref(props.duration* 1000)
const timerString= ref("")
let timer ;
const changeTimer =() => {
    console.log(duration.value)
    duration.value -= 1000
    const minutes = Math.floor(duration.value / 60000)
    const seconds =Math.floor(duration.value % 60000)/1000
    const beautifyMinutes =  minutes < 10 ? "0"+ minutes: minutes
    const beautifySeconds =  seconds < 10 ? "0"+ seconds: seconds
    timerString.value = `${beautifyMinutes}:${beautifySeconds}`
    if(!minutes && !seconds) emit('endTimer')
}
onMounted(() => {
    timer = setInterval(changeTimer,1000)
})
onUnmounted(() => {
    clearInterval(timer)
})
</script>

<template>
    <div class="timer-component">
        <p>
            {{timerString}}
        </p>
    </div>
</template>

<style scoped>
.timer-component{
    background-color: #C3250E;
    border-radius: 5px;
    font-size: 13px;
    line-height: 16px;
    padding: 4px;
}
</style>
