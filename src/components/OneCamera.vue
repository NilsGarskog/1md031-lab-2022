<template>
  <div>
    <h3>{{ camera.name }}</h3>
    <p>Antal beställa: {{amountOrdered}}</p>
    <button id="addButton" v-on:click = "addOrder">Add order</button>
    <button id="removeButton" v-on:click = "removeOrder">Remove order</button>
    <br/>
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
    camera: Object
  },
    data: function () {
    return {
      amountOrdered: 0,
    };
},
methods: {
  addOrder: function() {
        this.amountOrdered += 1
        this.$emit('orderedCamera', { name:   this.camera.name, 
                                      amount: this.amountOrdered 
                                    }
  );
    },
  removeOrder: function() {
    this.amountOrdered -= 1
            this.$emit('orderedCamera', { name:   this.camera.name, 
                                      amount: this.amountOrdered 
                                    }
  );
  }
}
}
</script>
  
  <!-- Add "scoped" attribute to limit CSS to this component only -->
  <style scoped>

#addButton{
  background-color: aqua;
}
#removeButton{
  background-color: red;
}
</style>
  