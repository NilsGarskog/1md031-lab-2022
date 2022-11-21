<template>
  <div id="orders">
    <div id="orderList">
      <div
        v-for="(order, key) in orders"
        v-bind:key="'order' + key"
      >
        #{{ key }}:
        <span
          v-for="(item, amount, index) in order.orderItems"
          v-bind:key="'item' + amount"
        >
          <span id="camerasOrder" v-if="item !== 0"
            >{{ item }}pc {{ amount }} <span v-if="index != Object.keys(order.orderItems).length - 1">, </span>
          </span></span
        >
        <div id="infoOrder">
                  {{ order.details.name }} ({{ order.details.mail }},
        {{ order.details.pay }}, {{ order.details.gender }})
        </div>
        <span>
          <p> Order status: {{orderStatus}} </p>
          <button class="button-3" id="in-progress" v-on:click = "changeStatus('in_progress')">In progress</button>
          <button class="button-3" id="done" v-on:click = "changeStatus('done')">Done</button>
          </span>
        <hr>
      </div>
      <button v-on:click="clearQueue">Clear Queue</button>
    </div>
    <div
      id="dots"
      v-bind:style="{
        background: 'url(' + require('../../public/img/polacks.jpg') + ')',
      }"
    >
      <div id="dotText"
        v-for="(order, key) in orders"
        v-bind:style="{
          left: order.details.x + 'px',
          top: order.details.y + 'px',
        }"
        v-bind:key="'dots' + key"
      >
        {{ key }}
      </div>
    </div>
  </div>
</template>
  <script>
import io from "socket.io-client";
const socket = io();

export default {
  name: "DispatcherView",
  data: function () {
    return {
      orders: null,
      orderStatus: "Orderd"
    };
  },
  created: function () {
    socket.on("currentQueue", (data) => (this.orders = data.orders));
  },
  methods: {
    clearQueue: function () {
      socket.emit("clearQueue");

    },
    changeStatus: function(status){
      if (status === 'in_progress'){
        this.orderStatus = "In progress"
      }
      if (status === 'done'){
        this.orderStatus = "Done"
      }
      socket.emit("changedStatus", this.orderStatus)

    }
  },
};
</script>
  <style>
#orderList {
  top: 1em;
  left: 1em;
  position: absolute;
  z-index: 2;
  color: black;
  background: rgba(255, 255, 255, 0.5);
  padding: 1em;
}
#dots {
  position: relative;
  margin: 0;
  padding: 0;
  background-repeat: no-repeat;
  width: 1920px;
  height: 1078px;
  cursor: crosshair;
}

#dots div {
  position: absolute;
  background-image: url("https://cdn-icons-png.flaticon.com/512/684/684908.png");
  background-size: 40px 40px;
  color: rgb(3, 47, 68);
  font-weight: bold;
  border-radius: 10px; 
  width: 40px;
  height: 40px;
  text-align: justify;
}
#dotText{
  margin-bottom: 40px;

}
#infoOrder {
  font-style: italic;
}
#camerasOrder{
 font-weight: bold;
}
#in-progress{
  background-color: yellow;
  color: black;
}
#in-progress:hover {
  background-color: yellow;
}

#done{
  background-color: green;
  color: white;
}
</style>
  