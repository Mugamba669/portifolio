<template>
  <Renderer ref="rendererC" antialias :orbit-ctrl="{ enableDamping: true }" resize="window">
    <Camera :position="{ z: 10 }" />
    <Scene>
      <PointLight :position="{ y: 50, z: 50 }" />
      <Box :size="5" ref="meshC" :rotation="{ y: Math.PI / 4, z: Math.PI / 4 }">
        <LambertMaterial />
      </Box>
    </Scene>
  </Renderer>
</template>


<script lang="ts">
import { Box, Camera, LambertMaterial, MeshPublicInterface, PointLight, Renderer, RendererPublicInterface, Scene } from 'troisjs';
import Vue from 'vue';
export default Vue.extend({
  name: 'HelloWorld',
  components:{
    Box, Camera,LambertMaterial,PointLight,Renderer,Scene
  },
  props: {
    msg: String,
  },
  data(){
    return{
    render: this.$refs['rendererC'],
    meshC:this.$refs['meshC']
    }
  },
  mounted(){
  const renderer = this.render as unknown as RendererPublicInterface;
  const mesh = (this.meshC as unknown  as MeshPublicInterface).mesh;
  renderer.onBeforeRender(() => {
    mesh!.rotation.x += 0.01
  })
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
body, html {
  margin: 0;
}
canvas {
  display: block;
}
</style>
