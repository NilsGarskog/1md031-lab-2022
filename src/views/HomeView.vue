<template>
  <div>
    <header>
      <img
        src="https://images-wixmp-ed30a86b8c4ca887773594c2.wixmp.com/f/549e9b77-4c90-4c7f-8d0e-772a4ba70576/dbbpqj5-dfbf4e9d-e4d9-4c1c-81c6-fd8511db78d0.jpg/v1/fill/w_1192,h_670,q_70,strp/tokyo_street_night_by_arsenixc_dbbpqj5-pre.jpg?token=eyJ0eXAiOiJKV1QiLCJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ1cm46YXBwOjdlMGQxODg5ODIyNjQzNzNhNWYwZDQxNWVhMGQyNmUwIiwiaXNzIjoidXJuOmFwcDo3ZTBkMTg4OTgyMjY0MzczYTVmMGQ0MTVlYTBkMjZlMCIsIm9iaiI6W1t7ImhlaWdodCI6Ijw9MTA4MCIsInBhdGgiOiJcL2ZcLzU0OWU5Yjc3LTRjOTAtNGM3Zi04ZDBlLTc3MmE0YmE3MDU3NlwvZGJicHFqNS1kZmJmNGU5ZC1lNGQ5LTRjMWMtODFjNi1mZDg1MTFkYjc4ZDAuanBnIiwid2lkdGgiOiI8PTE5MjAifV1dLCJhdWQiOlsidXJuOnNlcnZpY2U6aW1hZ2Uub3BlcmF0aW9ucyJdfQ.CNVuy3GnEPntjZ8e1EUhzhxBtnpBC6ZLV42ApeeVZ1k"
        id="headlineIMG"
      />
      <h1 id="Header">NILS CAMERAS</h1>
    </header>
    <main>
      <section id="cameras">
        <h2>Cameras</h2>
         <!--
        <p>Current delivery time is {{deliveryTime}}</p>
        -->
        <div class="wrapper">
          <Camera
            v-for="camera in cameras"
            v-bind:camera="camera"
            v-bind:key="camera.name"
            v-on:orderedCamera="addToOrder($event)"
          />

          <!--<div class="box a">
            <h3>M10</h3>
            <img src="img/M10.jpg" style="width: 200px; height: 200px" />
            <ul>
              <li>Rangefinder</li>
              <li>Leica <span id="mount">M mount</span></li>
            </ul>
          </div>
          <div class="box b">
            <h3>Q2</h3>
            <img src="img/Q2.jpg" style="width: 200px; height: 200px" />
            <ul>
              <li>Compact camera</li>
              <li>Integrated <span id="mount">Summilux 28/1.7</span></li>
            </ul>
          </div>
          <div class="box c">
            <h3>SL2</h3>
            <img src="img/SL2.jpg" style="width: 200px; height: 200px" />
            <ul>
              <li>System camera</li>
              <li><span id="mount">L mount</span></li>
            </ul>
          </div>-->
        </div>
        <!--
        <button v-on:click = "checkDeliveryTime">Delivery time</button>
        -->
      </section>
      <section id="Customer_information">
        <h2>Customer information</h2>
        <section id="contact">
          <p>Please fill in your information </p>
          <form>
            <p>
              <label for="Fullname">Full name</label><br />
              <input
                type="text"
                id="firstname"
                v-model="fn"
                required="required"
                placeholder="Full name"
              />
            </p>
            <p>
              <label for="email">Email</label><br />
              <input
                type="email"
                id="email"
                v-model="em"
                required="required"
                placeholder="E-mail address"
              />
            </p>
            <p>
              <label for="Payment">Payment</label>
              <select v-model="pay">
                <option>Swish</option>
                <option>Check</option>
                <option>Paypal</option>
                <option>Card</option>
              </select>
            </p>
            <p>Gender</p>
            <div>
              <input
                type="radio"
                id="Male"
                v-model="g"
                value="Male"
                checked
              />
              <label for="Male">Male</label>
            </div>
            <div>
              <input 
                type="radio" 
                id="Femalre"
                v-model="g"
                value="Female" 
              />
              <label for="Female">Female</label>
            </div>
            <div>
              <input 
                type="radio"
                id="Other"
                v-model="g"
                value="Other"
              />
              <label for="Other">Other</label>
            </div>
             <p>Click on the delivery adress in the map below</p>
                <div id="fitMap">
              <div id="map" v-on:click="setLocation" v-bind:style="{ background: 'url(' + require('../../public/img/polacks.jpg')+ ')' }">
                <div v-bind:style="{ left: location.x + 'px', top: location.y + 'px'}" v-bind:key="'dots' + key">
             T
          </div>
    </div>
    </div>
          </form>
        </section>
      </section>
    </main>
    <button class="button-3" role="button" type="submit" v-on:click = "printInformation">
      {{orderText}}
    </button>
    <hr />
    <footer>&#169; Nils</footer>
  </div>
</template>

<script>
import Camera from "../components/OneCamera.vue";
import menu from "../assets/menu.json";
import io from "socket.io-client";

const socket = io();

/* Gammla konstruktorn
function MenuItem(pN, im, cT, m) {
  this.name = pN;
  this.image = im;
  this.cameraType = cT;
  this.mount = m;
}

const Camera1 = new MenuItem("M10", "img/M10.jpg", "Rangefinder", "M mount");
const Camera2 = new MenuItem(
  "Q2",
  "img/Q2.jpg",
  "Comapct camera",
  "Fixed lens"
);
const Camera3 = new MenuItem("SL2", "img/SL2.jpg", "System camera", "L mount");

const Products = [Camera1, Camera2, Camera3];

*/
export default {
  name: "HomeView",
  components: {
    Camera,
  },
  data: function () {
    return {
      cameras: menu,
      fn: "",
      em: "",
      pay: "Card",
      g: "",
      orderedCameras: {},
      deliveryTime: 0,
      location: { x: 0,
            y: 0
          },
      orderText: "Order"

    };
  },
      created: function () {
      socket.on('DeliveryTimeIs', time =>
        this.deliveryTime = time);
    },
  methods: {
    printInformation: function() {
        this.orderText = "Thank you!"
        console.log(this.fn, this.em, this.pay, this.g, this.orderedCameras)
        socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: {
          x: this.location.x,
          y: this.location.y,
          name: this.fn,
          mail: this.em,
          pay: this.pay,
          gender: this.g,
        },
        orderItems: this.orderedCameras,
      });
    },
    getOrderNumber: function () {
      return Math.floor(Math.random() * 100000);
    },
    /*
    addOrder: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top,
      };
      this.location.x = event.clientX - 10 - offset.x;
      this.location.y = event.clientY - 10 - offset.y;
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: {
          x: event.clientX - 10 - offset.x,
          y: event.clientY - 10 - offset.y,
        },
        orderItems: ["Beans", "Curry"],
      });
    },
   */
    addToOrder: function (event) {
  this.orderedCameras[event.name] = event.amount;
    },

    checkDeliveryTime: function () {  //TA BORT SEN
        socket.emit("deliveryTime")
        console.log("skickat delivery")
    },

    setLocation: function(event) {
            var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top,
      };
      this.location.x = event.clientX - 10 - offset.x;
      this.location.y = event.clientY - 10 - offset.y;
    }
  },
};
</script>

<style>
@import "https://fonts.googleapis.com/css?family=specimen|Questrial";

body {
  /* Sätta allmänna regler för all text */
  font-family: "Questrial", specimen;
  text-align: center;
}

#mount {
  text-transform: uppercase;
  font-weight: bold;
}

#Customer_information {
  background-color: black;
  color: white;
  margin: 10px 25px;
  border: 10px solid rgba(255, 255, 255, 0.822);
  border-radius: 25px;
  border-radius: 10px;
  border-style: inset;
}

#cameras {
  margin: 10px 25px;
  border: 10px solid rgba(21, 82, 21, 0.822);
  border-radius: 25px;
  border-style: outset;
}

li {
  text-align: left;
}


.button-3 {          /* Knapp utseende hämtat från github via "getcssscan.com" */
  appearance: none;
  height: 40px;
  background-color: #2ea44f;
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

.button-3:focus:not(:focus-visible):not(.focus-visible) {
  box-shadow: none;
  outline: none;
}

.button-3:hover {
  background-color: #2c974b;
}

.button-3:focus {
  box-shadow: rgba(46, 164, 79, .4) 0 0 0 3px;
  outline: none;
}

.button-3:disabled {
  background-color: #94d3a2;
  border-color: rgba(27, 31, 35, .1);
  color: rgba(255, 255, 255, .8);
  cursor: default;
}

.button-3:active {
  background-color: #298e46;
  box-shadow: rgba(20, 70, 32, .2) 0 1px 0 inset;
}


button:hover {
  background-color: green;
  cursor: pointer;
  transition: background-color 0.3s;
}

#headlineIMG {
  position: relative;
  opacity: 0.7;
  object-fit: cover;
  height: 200px;
  width: 100%;
  filter: blur(3px);
  -webkit-filter: blur(3px);
}

#Header {
  text-align: center;
  width: 100%;
  position: absolute;
  margin-top: -150px;
  font-weight: bold;
  font-size: 80px;
}

/*Grid structure*/
.wrapper {
  display: grid;
  grid-template-columns: 33% 33% 33%;
}

#map{
    width: 1920px;
    height: 1078px;
    background-color: red;
    position: relative;
    background-repeat: no-repeat;
    cursor: crosshair;
}
#fitMap{
  overflow: scroll;
  height: 600px;
  width: 1200px;
  display: block;
  margin-left: auto;
  margin-right: auto; 
  margin-bottom: 30px;
}
  #map div {
    position: absolute;
    background: black;
    color: white;
    border-radius: 10px;
    width:20px;
    height:20px;
    text-align: center;
  }

/*empty*/
</style>