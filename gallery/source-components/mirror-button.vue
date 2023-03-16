<template>
  <div :class="['button-wrap', buttonPressed ? 'pressed' : null]">
    <div :class="['button', buttonPressed ? 'pressed': null]">
      <video  ref="videoRef"></video>
    </div>
    <div className="text">Text</div>
  </div>
  <button @click="close" >关闭</button>
  <button @click="open" >开启</button>
</template>

<script lang="ts" setup>
import {ref,onBeforeUnmount} from 'vue';


const buttonPressed = ref(false);
const videoRef = ref()

const close = () => {
  videoRef.value.srcObject.getTracks()[0].stop()
  buttonPressed.value = false
}
const open = () => {
  navigator.mediaDevices.getUserMedia({
  video: true,
})
.then((stream) => {
  videoRef.value.srcObject = stream;
  videoRef.value.onloadedmetadata = () => {
    videoRef.value.play()
  }
  buttonPressed.value = true;
})
.catch((e) => console.log(e));
}

open()

onBeforeUnmount(() => {
  videoRef.value.srcObject?.getTracks()[0].stop()
})
</script>

<style lang="scss" scoped>
video {
  width: 300px;
  height: 200px;
  object-fit: cover;
  object-position: 0 0px;
  filter: blur(2px) saturate(0.6) brightness(1.1);//饱和度 亮度
  transform: scaleX(-1);
}
:root {
  --transition: 0.1s;
  --border-radius: 56px;
}

.button-wrap {
  width: 300px;
  height: 300px;
  position: relative;
  transition: transform var(--transition), box-shadow var(--transition);
}

.button-wrap.pressed {
  transform: translateZ(0) scale(0.95);
}

.button {
  width: 100%;
  height: 100%;
  border: 1px solid #fff;
  overflow: hidden;
  border-radius: var(--border-radius);
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.25), 0px 8px 16px rgba(0, 0, 0, 0.15),
    0px 16px 32px rgba(0, 0, 0, 0.125);
  transform: translateZ(0);
  cursor: pointer;
}

.button.pressed {
  box-shadow: 0px -1px 1px rgba(0, 0, 0, 0.5), 0px 1px 1px rgba(0, 0, 0, 0.5);
}

.text {
  position: absolute;
  left: 50%;
  top: 50%;
  transform: translate(-50%, -50%);
  pointer-events: none;
  color: rgba(0, 0, 0, 0.7);
  font-size: 48px;
  font-weight: 500;
  text-shadow:0px -1px 0px rgba(255, 255, 255, 0.5),0px 1px 0px rgba(255, 255, 255, 0.5);
}

button{
  color:pink
}

</style>