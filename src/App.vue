<template>
  <div class="h-screen p-20 bg-gray-100">
    <div class="w-72">
      <Listbox ref="listbox" v-model="selectedPerson" as="div">
        <ListboxLabel
          class="block mb-1 text-sm font-medium text-gray-700 truncate"
          >Focusable Listbox</ListboxLabel
        >
        <div class="relative">
          <ListboxButton
            ref="listboxButton"
            class="relative w-full py-2 pl-3 pr-10 text-sm text-left bg-white border border-gray-300 rounded shadow-sm cursor-pointer  focus:outline-none focus:ring-1 focus:ring-opacity-75 focus:border-opacity-75 focus:ring-blue-700 focus:border-blue-700"
          >
            <span class="block truncate">{{ selectedPerson.name }}</span>
            <span
              class="absolute inset-y-0 right-0 flex items-center pr-2 pointer-events-none "
            >
              <SelectorIcon class="w-5 h-5 text-gray-400" aria-hidden="true" />
            </span>
          </ListboxButton>

          <transition
            leave-active-class="transition duration-100 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
          >
            <ListboxOptions
              class="absolute z-10 w-full py-1 mt-1 overflow-auto text-base bg-white rounded-md shadow-lg  max-h-60 ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm"
            >
              <ListboxOption
                v-for="(person, index) in people"
                v-slot="{ active, selected }"
                :key="index"
                :value="person"
                as="template"
              >
                <li
                  :class="[
                    active ? 'text-blue-900 bg-blue-100' : 'text-gray-900',
                    'cursor-default select-none relative py-2 pl-10 pr-4',
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
                    class="absolute inset-y-0 left-0 flex items-center pl-3  text-amber-600"
                  >
                    <CheckIcon class="w-5 h-5" aria-hidden="true" />
                  </span>
                </li>
              </ListboxOption>
            </ListboxOptions>
          </transition>
        </div>
      </Listbox>
    </div>
    <button
      type="button"
      class="
        mt-10
        mr-2
        inline-flex
        items-center
        px-2.5
        py-1.5
        border border-gray-300
        shadow-sm
        text-xs
        font-medium
        rounded
        text-gray-700
        bg-white
        hover:bg-gray-50
        focus:outline-none
        focus:ring-2 focus:ring-blue-500
      "
      @click="focusListbox()"
    >
      Focus Listbox
    </button>
    <button
      type="button"
      class="
        mt-10
        inline-flex
        items-center
        px-2.5
        py-1.5
        border border-gray-300
        shadow-sm
        text-xs
        font-medium
        rounded
        text-gray-700
        bg-white
        hover:bg-gray-50
        focus:outline-none
        focus:ring-2 focus:ring-blue-500
      "
      @click="focusListboxButton()"
    >
      Focus Listbox Button
    </button>
  </div>
</template>

<script lang="ts">
import { ComponentPublicInstance, defineComponent, ref } from 'vue'
import {
  Listbox,
  ListboxLabel,
  ListboxButton,
  ListboxOptions,
  ListboxOption,
} from '@headlessui/vue'
import { CheckIcon, SelectorIcon } from '@heroicons/vue/solid'

export default defineComponent({
  name: 'App',
  components: {
    Listbox,
    ListboxLabel,
    ListboxButton,
    ListboxOptions,
    ListboxOption,
    CheckIcon,
    SelectorIcon,
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

    const listbox = ref<ComponentPublicInstance>()
    const listboxButton = ref<ComponentPublicInstance>()

    function focusListbox() {
      listbox.value?.$el.focus()
      console.log(document.activeElement)
    }

    function focusListboxButton() {
      listboxButton.value?.$el.focus()
      console.log(document.activeElement)
    }

    return {
      people,
      selectedPerson,
      listbox,
      listboxButton,
      focusListbox,
      focusListboxButton,
    }
  },
})
</script>
