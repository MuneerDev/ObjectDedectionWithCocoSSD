<script setup>
import { defineProps,ref } from 'vue';
const props = defineProps({
  box: Object
})
const x = ref(String(Math.round(props.box.bbox[0])))
const y = ref(String(Math.round(props.box.bbox[1])))
const width = ref(String(Math.round(props.box.bbox[2])))
const height = ref(String(Math.round(props.box.bbox[3])))


</script>

<template>
  <div :style="{left:`${x}px`,top:`${y}px`,backgroundColor:'#4ade80',position:'absolute', width: `${width}px`, height: `${height}px`, opacity: '0.5'}">
    <p class="absolute top-[-8%] text-gray-700 left-0 bg-slate-200">{{ box.class }}</p>
  </div>
</template>



