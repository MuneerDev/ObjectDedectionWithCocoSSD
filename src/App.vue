<template>
  <div class="mx-auto w-fit mt-10">
    <div class="relative overflow-hidden w-[500px] h-[350px] mb-6">
<video @loadeddata="predect"  width="600" height="800" ref="video" class=" w-[500px] h-[350px]  bg-black">
</video>
<Box v-for="Box in Objects" :box="Box"></Box>
</div>
<button @click="openCam" class="mr-3 bg-black text-white px-3 py-2 rounded-lg">Open Cam</button>
<button @click="closeCam" class="bg-black text-white px-3 py-2 rounded-lg">Close Cam</button>
</div>
</template>

<script setup>
import Box from "./components/objectDedect.vue"
import { ref } from 'vue';
import { model } from "./AI"

const video = ref()
const Objects = ref([])
let mediaStream = null
const openCam = () =>{
  navigator.mediaDevices.getUserMedia({
    video: true,
    audio: false
  }).then(stream => {
    mediaStream = stream
    video.value.srcObject = stream
    video.value.play()
  })
}

const closeCam = () =>{
  mediaStream.getTracks().forEach(track => track.stop())
  mediaStream = null
}

const predect = () =>{
  model.detect(video.value).then(e => {
    Objects.value = e
    console.log(e[0])
  })
  if(mediaStream !== null){
      Objects.value = []
    window.requestAnimationFrame(predect)
  }
}
</script>


