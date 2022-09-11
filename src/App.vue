<script setup lang="ts">
import {ref} from 'vue'
import InputBirthday from './components/input-birthday.vue'
import LifeBoxs from './components/life-boxs.vue'

const weeks = ref(null);
</script>

<template>
  <header class="flex flex-col md:flex-row md:flex-row-reverse items-center">
    <figure class="logo-wrap mb-2 md:mb-0">
      <img src="/assets/duck.jpg" class="logo" alt="Vite logo" />
    </figure>
    <h1 class="text-4xl md:text-5xl mr-0 md:mr-2">나는 인생 <br class="md:hidden"/> <span class="text-yellow-300">{{weeks ?? 'N'}}</span>주차 입니다</h1>
  </header>
  <input-birthday @get-weeks="weeks = $event"/>
  <life-boxs v-if="weeks" :weeks="weeks"/>
  <footer class="flex flex-col read-the-docs mt-4">
    <a href="https://github.com/programmer-heeney/your-life" target="_blank">See the code on Github.</a>
    <span class="source">
      이미지: 
      <a  href="https://kr.freepik.com/free-vector/duck-wearing-a-dinosaur-costume-cartoon-illustration_12781717.htm#query=character&position=0&from_view=keyword">작가 mamewmy</a> 
      출처 Freepik
    </span>
  </footer>
</template>

<style scoped>
.logo-wrap{
  width: 150px;
  height: 150px;
  border-radius: 50%;
  overflow: hidden;
}
.logo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  will-change: filter;
}
.logo-wrap:hover {
  filter: drop-shadow(0 0 2em #42b883aa);
}
.source {
  font-size: 15px;
}
.read-the-docs {
  color: #888;
}
.read-the-docs:hover{
  color: white;
}
</style>
