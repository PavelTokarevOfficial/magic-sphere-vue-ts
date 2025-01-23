<template>
  <div class="wrapper">
    <div class="gradient"></div>
    <SelectLang class="absolute top-[20px] right-[20px]" :values="languages" @change="changeLang"/>
    <Sphere class="relative top-[50%] left-[50%] translate-y-[-50%] translate-x-[-50%] z-10" :items="phrases" :selectLang="lang"/>
  </div>
</template>

<script setup lang="ts">
import {ref} from "vue";
import Sphere from "@/components/Sphere.vue";
import SelectLang from "@/components/SelectLang.vue";
import {languages} from '@/constants/languages.ts'
import {phrases} from '@/constants/phrases.ts'
import type {TLanguage} from '@/types/languages.ts'

const lang = ref<TLanguage>(languages[0])

const changeLang = (newLang: TLanguage) => {
  lang.value = newLang
}
</script>