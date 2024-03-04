<script setup>
import { OrbitControls } from '@tresjs/cientos'

import { TresCanvas } from '@tresjs/core'

const boxRef = ref(null);

const { onLoop } = useRenderLoop();

onLoop(({ delta, elapsed }) => {
  if (boxRef.value) {
    boxRef.value.rotation.y += delta
    boxRef.value.rotation.z = elapsed * 0.2
  }
})
</script>

<template>
  <div>
    <!-- <NuxtWelcome /> -->
    <TresCanvas
      clear-color="#82DBC5"
      window-size>
    <!-- Your scene here -->
      <TresPerspectiveCamera 
        :position="[3, 3, 3]"
        :look-at="[0, 0, 0]"/>

      <TresMesh
        ref="boxRef"
        :scale="1">

        <TresTorusGeometry :args="[1, 0.5, 16, 32]" />
        <TresMeshBasicMaterial color="orange" />
      </TresMesh>
      <TresAmbientLight :intensity="1" />

      <OrbitControls />
    </TresCanvas>
  </div>
</template>

<style>
html,
body {
  margin: 0;
  padding: 0;
  height: 100%;
  width: 100%;
}
#app {
  height: 100%;
  width: 100%;
}
</style>