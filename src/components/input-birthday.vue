<script setup lang="ts">
import { ref, watch } from 'vue'
import moment from 'moment'

const emits = defineEmits(['getWeeks'])

const today = moment();
const date = ref(null);
const userLocale = navigator.language;

const clickInput = () => {
  const calendar:any = document.querySelector('.vc-popover-content');
  emits('getWeeks', date.value ? today.diff(date.value, 'week') : null);
  setTimeout(()=> {
    if(calendar) calendar.style.display = 'none';
  }, 0)
}

watch(() => date.value, (newVal :any) => {
  if(!newVal) return clickInput();
})
</script>

<template>
  <div class="w-full max-w-sm m-auto mt-2">
    <form class="bg-white rounded px-8 pt-6 pb-8" @submit.prevent>
      <label class="block text-gray-600 text-sm text-left font-bold mb-2" for="date">
        π μλμμΌμ μλ ₯νμΈμ
        <span class="text-sm text-gray-400">{{moment().endOf('month').format('L')}}</span>
      </label>
      <div class="flex flex-col md:flex-row">
        <v-date-picker v-model="date" :locale="userLocale" class="flex-grow" color="green" is-dark> 
          <template v-slot="{ inputValue, inputEvents }">
            <input
              id="date"
              class="bg-white text-gray-700 w-full py-2 px-3 appearance-none border rounded-l focus:outline-none"
              :value="inputValue"
              :placeholder="moment().endOf('month').format('L')"
              v-on="inputEvents"
              @keyup.enter.prevent="clickInput"
            />
          </template>
        </v-date-picker>
        <button
          type="button"
          class="text-white font-bold py-2 px-4 rounded user-select-none focus:outline-none mt-2 md:mt-0 md:ml-2"
          :class="date ? 'bg-green-500' : 'bg-green-300'"
          :disabled="!date"
          @click="clickInput"
        >
          μλ ₯
        </button>
      </div>
    </form>
  </div>
</template>

<style scoped>
</style>
