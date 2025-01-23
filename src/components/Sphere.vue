<template>
  <button
      class="sphere relative bg-black w-[350px] lg:w-[600px] h-[350px] lg:h-[600px] rounded-[50%]"
      @click="getRandomPhrases"
  >
    <span
        :class="[
            animate ? 'sphere__animation' : '' ,
            'absolute w-[200px] lg:w-[350px] h-[170px] lg:h-[290px] p-[25px] lg:p-[60px] bg-white rounded-[50%] ' +
             'translate-x-[-50%] top-[30px] lg:top-[40px] left-[50%] text-gray-700'
        ]"
    >
      {{ ans }}
    </span>
  </button>
</template>

<script setup lang="ts">
import {defineProps, ref} from 'vue'
import type {TPhrase} from '@/types/phrases.ts'
import type {TLanguage} from '@/types/languages.ts'

const props = defineProps<{
  items: TPhrase[],
  selectLang: TLanguage
}>()

const animate = ref<boolean>(false)
const ans = ref<string>('Нажми')

const getRandomPhrases = () => {
  animate.value = true

  setTimeout(() => {
    const randomIndex = Math.floor(Math.random() * props.items.length);
    const lang = props.selectLang.name as keyof TPhrase;
    ans.value = props.items[randomIndex][lang] as string;
    animate.value = false;
  }, 2000);
};
</script>