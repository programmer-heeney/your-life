<script setup lang="ts">
interface Props {
    weeks: any;
}
const props = defineProps<Props>();

const YEARS = 91;
const WEEKS_A_YEAR = 52;

const isBeforeCurrent = (year:number, week:number) => ((((year-1)*WEEKS_A_YEAR) + week) <= props.weeks)

</script>
<template>
    <ul class="flex flex-col mt-10">
        <li v-for="year in YEARS" :key="year" class="flex items-center">
            {{year-1 < 10 ? `0${year-1}`:year-1}}
            <div v-for="week in WEEKS_A_YEAR" :key="week" class="w-[5px] h-[5px] m-1 group"
            :class="{'bg-green-900': isBeforeCurrent(year, week), 'bg-yellow-300': week%5 === 0, 'bg-stone-500': !isBeforeCurrent(year, week)}"
            >
                <div class="relative bottom-[30px] flex flex-col items-center hidden mb-6 group-hover:flex">
                    <span class="relative z-10 p-2 text-xs leading-none text-white whitespace-no-wrap bg-black shadow-lg">{{(((year-1)*WEEKS_A_YEAR) + week)}}</span>
                    <div class="w-3 h-3 -mt-2 rotate-45 bg-black"></div>
                </div>  
            </div>
        </li>
    </ul>
</template>