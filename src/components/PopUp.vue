<template>
  <div class="PopUp">
    <div class="popupinner">
        <slot />
        <h2>Thank you for your order!</h2>
        <h3>Order information</h3>
          <div>
          <p>Name: {{Receipt[0]}}</p>
          <p>E-mail: {{Receipt[1]}}</p>
          <p>Payment method: {{Receipt[2]}}
          <p>Products:</p>
          <div v-for="(item, amount) in Receipt[5]" v-bind:key="'item' + amount">
            {{ item }}pc {{ amount }}
          </div>
          <p>Order number: #{{Receipt[4]}}</p>
          </div>
          <p>Order status:</p>
          <div id="orderd" v-if="orderStatus === 'Orderd'">{{orderStatus}}</div>
          <div id="in-progress" v-if="orderStatus === 'In progress'">{{orderStatus}}</div>
          <div id="done" v-if="orderStatus === 'Done'">{{orderStatus}}</div>
           <hr />
        <button class ="popup-close" v-on:click="closePopup">
            Close
        </button>
    </div>
  </div>
</template>

<script>
import io from "socket.io-client";
const socket = io();

export default {

  props: ['Receipt'],
  data: function () {
    return{
      orderStatus: "Orderd",
    }
  },
  methods:{
  closePopup: function() {
    this.$emit('closeCurrentPopup')
  }
  },
    created: function () {
      socket.on('currentStatus', status => this.orderStatus = status);
    },
}

</script>

<style scoped>
.PopUp{
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 99;
  background-color: rgba(0,0,0,0.7);

  display: flex;
  align-items: center;
  justify-content: center;
}
    .popupinner{
      background: #FFF;
      padding: 32px;
    }

.popup-close {          /* Knapp utseende hämtat från github via "getcssscan.com" */
  appearance: none;
  height: 40px;
  background-color: red;
  border: 1px solid rgba(27, 31, 35, .15);
  border-radius: 6px;
  box-shadow: rgba(27, 31, 35, .1) 0 1px 0;
  box-sizing: border-box;
  color: #fff;
  cursor: pointer;
  display: inline-block;
  font-family: -apple-system,system-ui,"Segoe UI",Helvetica,Arial,sans-serif,"Apple Color Emoji","Segoe UI Emoji";
  font-size: 14px;
  font-weight: 600;
  line-height: 20px;
  padding: 6px 16px;
  position: relative;
  text-align: center;
  text-decoration: none;
  user-select: none;
  -webkit-user-select: none;
  touch-action: manipulation;
  vertical-align: middle;
  white-space: nowrap;
  display: inline-block;
}

.popup-close:focus:not(:focus-visible):not(.focus-visible) {
  box-shadow: none;
  outline: none;
}

.popup-close:hover {
  background-color: rgb(155, 1, 1);
}

.popup-close:focus {
  box-shadow: rgba(164, 89, 46, 0.4) 0 0 0 3px;
  outline: none;
}

.popup-close:disabled {
  background-color: #d3a394;
  border-color: rgba(27, 31, 35, .1);
  color: rgba(255, 255, 255, .8);
  cursor: default;
}

.popup-close:active {
  background-color: #8e6229;
  box-shadow: rgba(20, 70, 32, .2) 0 1px 0 inset;
}


button:hover {
  background-color: rgb(128, 83, 0);
  cursor: pointer;
  transition: background-color 0.3s;
}

#orderd {
  background-color: grey;
  color: white;

}

</style>