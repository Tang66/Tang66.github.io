<template>
  <span ref="imgRef" @mousewheel="rollImg">
    <User style="width: 100px;height: 100px;" />
  </span>
</template>

<script lang="ts" setup>
import { ref } from 'vue';

const imgRef = ref()

const rollImg = ( event: any ) => {
  let zoom = parseInt( imgRef.value.style.zoom, 10 ) || 100;
  zoom += event.wheelDelta / 12;
  if ( zoom > 0 ) imgRef.value.style.zoom = zoom + '%';
  return false;
}; 
</script>