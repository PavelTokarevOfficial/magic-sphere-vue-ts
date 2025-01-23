<template>
  <div class="w-auto">
    <Listbox v-model="selectedIndex">
      <div class="relative mt-1 z-40">
        <ListboxButton
            class="min-w-[200px] relative cursor-default rounded-lg bg-white/50
            py-2 px-3 text-left focus:outline-none sm:text-sm"
        >
          <span class="block truncate">lang: {{ selectedValue.name }} </span>
        </ListboxButton>

        <transition
            leave-active-class="transition duration-100 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
        >
          <ListboxOptions
              class="absolute mt-1 max-h-60 min-w-[200px] overflow-auto rounded-md
               bg-white/50 py-1 text-base focus:outline-none sm:text-sm"
          >
            <ListboxOption
                v-slot="{ active, selected }"
                v-for="item in values"
                :key="item.name"
                :value="item.id"
                as="template"
            >
              <li
                  :class="[
                  active ? 'bg-amber-100 text-amber-900' : 'text-gray-900',
                  'relative cursor-default select-none py-2 px-3'
                  ]">
                <span :class="[selected ? 'font-medium' : 'font-normal','block truncate',]">{{ item.name }}</span>
              </li>
            </ListboxOption>
          </ListboxOptions>
        </transition>
      </div>
    </Listbox>
  </div>
</template>

<script setup lang="ts">
import {defineEmits, defineProps, ref, watch} from 'vue'
import {Listbox, ListboxButton, ListboxOption, ListboxOptions} from "@headlessui/vue";
import type {TLanguage} from '@/types/languages.ts'

const props = defineProps<{
  values: TLanguage[]
}>()

const emit = defineEmits<{
  (e: 'change', selected: TLanguage): void
}>()

const selectedIndex = ref<number>()
const selectedValue = ref<TLanguage>(props.values[0])

watch(selectedIndex, () => {
  selectedValue.value = props.values.find(item => item.id === selectedIndex.value) as TLanguage
  emit('change', selectedValue.value)
})
</script>