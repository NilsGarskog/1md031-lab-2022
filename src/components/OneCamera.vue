<template>
  <div>
    <h3>{{ camera.name }}</h3>
    <img v-bind:src= "camera.image" style="width: 200px; height: 200px">
    <ul>
      <li>{{ camera.cameraType }}</li>
      <li>Leica <span id="mount">{{ camera.mount }}</span></li>
    </ul>
  </div>
</template>

  <script>
export default {
  name: "OneCamera",
  props: {
    camera: Object,
  },
};
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>
</style>
  