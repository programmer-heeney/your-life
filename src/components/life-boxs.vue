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
    <ul class="flex flex-col mt-10 w-80 md:w-full">
        <span class="text-left md:hidden">만 0세 부터</span>
        <li v-for="year in YEARS" :key="year" class="flex items-center justify-between">
            <span class="hidden md:block">{{year-1 < 10 ? `0${year-1}`:year-1}}</span>
            <div v-for="week in WEEKS_A_YEAR" :key="week" class="w-[5px] h-[5px] mb-[2px] md:mb-0 group"
            :class="{'bg-green-900': isBeforeCurrent(year, week), 'bg-yellow-300': week%5 === 0, 'bg-stone-500': !isBeforeCurrent(year, week)}"
            >
                <div class="relative bottom-[45px] flex flex-col items-center hidden mb-6 group-hover:flex">
                    <span class="relative w-20 z-10 p-2 text-xs leading-none text-white whitespace-no-wrap bg-black shadow-lg">
                        {{`만 ${year-1}세:`}}<br/>
                        {{`${week}주차`}}
                    </span>
                    <div class="w-3 h-3 -mt-2 rotate-45 bg-black"></div>
                </div>  
            </div>
        </li>
        <span class="text-right md:hidden">만 91세 까지</span>
    </ul>
</template>