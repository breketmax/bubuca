<script setup lang="ts">
import {computed, defineProps, ref} from 'vue'
import Timer from "../Helpers/Timer.vue";

interface ICustomButton{
    type:  "Clear" | "Primary" | "Icon",
        text: string,
        icon: "close"|"heart"|"leftArrow"|"rightArrow"|"",
        iconPosition: "Right" | "Left" | ""
        timer: boolean
        duration:number
    size: "sm" | "md" | "lg"
    disabled:boolean
    waitText: string
}

const props = withDefaults(defineProps<ICustomButton>(),{
    type:"Primary",
    timer:false,
    iconPosition:"",
    duration:60,
    disabled:false,
    text: "",
    icon: "",
    size:"md",
    waitText:""
})
const imageUrl = computed(() => {
    return new URL(`../../assets/images/${props.icon}-${props.size}.svg`, import.meta.url).href
})
const isTimerStarted = ref(false)
const toggleTimer =() =>{
    isTimerStarted.value = !isTimerStarted.value
}
const withTimer = computed(() => {
    return isTimerStarted.value && props.timer
})
</script>

<template>
    <a :href="disabled? null : 'https://google.com'" target="_blank"  v-if="type=== 'Clear'">
        <button class="clear-button btn" :disabled="disabled">
            {{text}}
        </button>
    </a>

    <a :href="disabled  ? null : 'https://google.com'" target="_blank" :class="withTimer ? 'non-active' : ''"  v-if="type=== 'Primary'">
        <button class="primary-button btn" :disabled="disabled" @click="toggleTimer" >
            <div class="button-content">
                <img :src="imageUrl" alt="button-icon" v-if="iconPosition === 'Left' && icon">
                {{ withTimer? waitText: text }}
                <img :src="imageUrl" alt="button-icon" v-if="iconPosition === 'Right' && icon">
                <Timer v-if="withTimer" :duration="duration" @endTimer="toggleTimer"/>
            </div>
        </button>
    </a>

    <a :href="disabled? null : 'https://google.com'" target="_blank"  v-if="type=== 'Icon'" >
        <button class="icon-button btn" :disabled="disabled" :class="size">
            <div class="button-content">
                <img :src="imageUrl" alt="button-icon">
            </div>
        </button>
    </a>

</template>

<style scoped>
  .btn{
      font-weight: 400;
      font-size: 20px;
      line-height: 24px;
      transition: all .4s ease;
  }
  .btn:disabled{
      .button-content{
          opacity: 0.5;
      }
  }

  .clear-button{
      color: var(--primary-color);
  }
  .clear-button:hover{
      text-shadow: var(--text-shadow);
      background: var(--gradient-background);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      text-fill-color: transparent;
  }
  .clear-button:active{
      background: var(--active-background);
      -webkit-background-clip: text;
      -webkit-text-fill-color: transparent;
      background-clip: text;
      text-fill-color: transparent;
      text-shadow: none;
  }

  .primary-button,.icon-button{
      padding: 16px 24px;
      border-radius: 10px;
      background:var(--gradient-background);
      color:var(--white);
  }
  .primary-button:hover,.icon-button:hover{
      border-radius: 40px;
      box-shadow: var(--hover-shadow);
  }
  .primary-button:active,.icon-button:active{
      border-radius: 40px;
      background: var(--active-background);
      box-shadow: none;
  }
  .primary-button:disabled,.icon-button:disabled{
      background: var(--disable-background);
      color:var(--disable-color);
      pointer-events:none;
  }

  .icon-button{
      padding: 16px;
      border-radius: 10px;
  }
  .sm{
      padding: 12px;
  }

  .button-content{
      display: flex;
      column-gap: 8px;
      flex-direction: row;
      justify-content: center;
      align-items: center;
  }
  .non-active{
      pointer-events: none;
  }
</style>
