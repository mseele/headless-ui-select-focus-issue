<template>
  <label class="block">
    <span class="font-medium">{{ label }}</span>
    <Listbox v-slot="{ open }" v-model="selectedPerson">
      <div class="relative mt-1">
        <ListboxButton
          class="relative w-full py-2 pl-3 pr-10 text-left bg-white rounded border border-gray-300 cursor-pointer focus:outline-none focus:border-blue-600 focus:ring-blue-600 focus:ring-1"
        >
          <span class="block truncate">{{ selectedPerson.name }}</span>
          <span
            class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none"
          >
            <SelectorIcon class="w-5 h-5 text-gray-400" aria-hidden="true" />
          </span>
        </ListboxButton>
        <transition
          v-show="open"
          leave-active-class="transition duration-100 ease-in"
          leave-from-class="opacity-100"
          leave-to-class="opacity-0"
        >
          <ListboxOptions
            class="absolute w-full py-1 mt-1 overflow-auto text-base bg-white rounded shadow-lg max-h-60 ring-1 ring-black ring-opacity-10 focus:outline-none sm:text-sm"
          >
            <ListboxOption
              v-for="person in people"
              v-slot="{ active, selected }"
              :key="person"
              :value="person"
              as="template"
            >
              <li
                :class="[
                  active ? 'text-blue-900 bg-blue-100' : 'text-gray-900',
                  'cursor-pointer select-none relative py-2 pl-10 pr-4',
                ]"
              >
                <span
                  :class="[
                    selected ? 'font-medium' : 'font-normal',
                    'block truncate',
                  ]"
                  >{{ person.name }}</span
                >
                <span
                  v-if="selected"
                  class="absolute inset-y-0 left-0 flex items-center pl-3 text-blue-600"
                >
                  <CheckIcon class="w-5 h-5" aria-hidden="true" />
                </span>
              </li>
            </ListboxOption>
          </ListboxOptions>
        </transition>
      </div>
    </Listbox>
  </label>
</template>

<script lang="ts">
import { defineComponent, PropType, ref } from 'vue'
import {
  Listbox,
  ListboxButton,
  ListboxOptions,
  ListboxOption,
} from '@headlessui/vue'
import { Value } from '@/type'
import { CheckIcon, SelectorIcon } from '@heroicons/vue/solid'

export default defineComponent({
  components: {
    Listbox,
    ListboxButton,
    ListboxOptions,
    ListboxOption,
    CheckIcon,
    SelectorIcon,
  },
  props: {
    label: {
      type: String,
      default: '',
      required: true,
    },
    modelValue: {
      type: Object as PropType<Value<string>>,
      default: () => {
        return { proposal: '', items: [] }
      },
      required: true,
    },
  },
  setup() {
    const people = [
      { name: 'Wade Cooper' },
      { name: 'Arlene Mccoy' },
      { name: 'Devon Webb' },
      { name: 'Tom Cook' },
      { name: 'Tanya Fox' },
      { name: 'Hellen Schmidt' },
    ]
    const selectedPerson = ref(people[0])

    return {
      people,
      selectedPerson,
    }
  },
})
</script>
