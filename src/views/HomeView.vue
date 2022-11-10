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
        <p></p>
        <div class="wrapper">
          <Camera
            v-for="camera in cameras"
            v-bind:camera="camera"
            v-bind:key="camera.name"
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
              <label for="Streetname">Street</label><br />
              <input
                type="text"
                id="Streetname"
                v-model="sn"
                placeholder="Street name"
              />
            </p>
            <p>
              <label for="Housenumber">House</label><br />
              <input
                type="number"
                id="Housenumber"
                v-model="hn"
                required="required"
                placeholder="House number"
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
          </form>
        </section>
      </section>
    </main>
    <button type="submit" v-on:click = "printInformation">
      <img src="img/submit.png" style="width: 80px" />
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
      cameras: menu, //försökte manuellt omvandla menu men pga det redan var ett java-objekt vid import gav det error?
      fn: "",
      em: "",
      sn: "",
      hn: "",
      pay: "Card",
      g: ""

    };
  },
  methods: {
    printInformation: function() {
        console.log(this.fn, this.em, this.sn, this.hn, this.pay, this.g)
    },
    getOrderNumber: function () {
      return Math.floor(Math.random() * 100000);
    },
    addOrder: function (event) {
      var offset = {
        x: event.currentTarget.getBoundingClientRect().left,
        y: event.currentTarget.getBoundingClientRect().top,
      };
      socket.emit("addOrder", {
        orderId: this.getOrderNumber(),
        details: {
          x: event.clientX - 10 - offset.x,
          y: event.clientY - 10 - offset.y,
        },
        orderItems: ["Beans", "Curry"],
      });
    },
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

button:hover {
  background-color: green;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:active {
  opacity: 0.7;
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

/*empty*/
</style>