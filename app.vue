<script setup>
import { OrbitControls, vLightHelper } from '@tresjs/cientos'

import { TresCanvas } from '@tresjs/core'
// import { ref } from 'vue'

const boxRef = shallowRef(null);

const { onLoop } = useRenderLoop();

onLoop(({ delta, elapsed }) => {
  if (boxRef.value) {
    boxRef.value.rotation.y += delta
    boxRef.value.rotation.z = elapsed * 0.1
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
        :position="[0, 0, 20]"
        :look-at="[5, 0, 0]"/>

      <TresMesh
        ref="boxRef"
        :scale="1"
        :castShadow="true"
        :recieveShadow="true">

        <!-- <TresTorusGeometry :args="[1, 0.5, 16, 32]" /> -->
        <TresBoxGeometry :args="[1, 1, 1, 4, 4, 4]" />
        <!-- <TresMeshBasicMaterial color="orange" /> -->
        <!-- <TresMeshNormalMaterial color="orange" /> -->
        <!-- <TresMeshToonMaterial color="#049ef4" /> -->
        <TresMeshStandardMaterial color="#049ef4" />
      </TresMesh>

      <TresMesh 
        :position="[5, 0, 0]"
        :castShadow="true"
        :recieveShadow="true">
        <TresSphereGeometry :args="[2, 32, 16, 0, 6.283185307179586, 0, 3.141592653589793]" />
        <!-- <TresMeshBasicMaterial color="orange" wireframe /> -->
        <TresMeshStandardMaterial color="orange" />
      </TresMesh>

      <TresMesh 
        :position="[0, 0, -2.5]"
        :recieveShadow="true"
        :castShadow="true">
        <TresPlaneGeometry :args="[100, 100, 48, 48]" />
        <TresMeshStandardMaterial color="#ffffff" />
      </TresMesh>


      <!-- <TresAmbientLight :intensity="1" /> -->
      <!-- <TresDirectionalLight color="#FFFFFF" :intensity="1" :shadow="true" :cast-shadow="true" :position="[0, 0, 10]"/> -->
      <TresDirectionalLight ref="directionalLightRef" :args="['white', 1]" :position="[0, 0, 10]" v-light-helper/>

      <TresSpotLight color="#FFFFFF" :intensity="20" :distance="20" :decay="10" :position="[0, 20, 20]" :castShadow="true"/>

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