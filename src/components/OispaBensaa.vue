<template>
  <div class="row">
    <h1>{{ msg }}</h1>
    <div class="wrap">
      <section class="form">
        <h3> Valitse autosi bensan kulutus </h3>
        <div class="gas-container">
          <input type="radio" name="form.gas_button" id="3" value="3" v-model="form.gas_button">
          <label class="gas" for="3">3 l / 100km</label>
          <input type="radio" name="form.gas_button" id="3.5" value="3.5" v-model="form.gas_button">
          <label class="gas" for="3.5">3,5 l / 100km</label>
          <input type="radio" name="form.gas_button" id="4" value="4" v-model="form.gas_button">
          <label class="gas" for="4">4 l / 100km</label>
        </div>

        <div class="travel-container">
          <p> Matkan pituus? (km) </p>
          <div class="number-input">
            <input id="travel_input" class="quantity" type="number" min="0" v-model="form.travel_input">
          </div>

        </div>

        <h3> Vertailtavat keskinopeudet </h3>
        <div class="speed-container" id="speed-container">
          <div class="third">
            <p> Nopeus 1 (km/h) </p>
            <div class="number-input">
              <input id="speed_input_1" class="quantity" type="number" min="0" v-model="form.speed_input_1" @change="onChange($event)">
            </div>

            <div class="results" id="results_1">
              {{ (form.travel_input / 100 * (form.gas_button * 1.009 ** (form.speed_input_1))).toFixed(2) }}
            </div>
          </div>

          <div id="gimme" class="third">
            <img id="cash" src="../assets/cash.png" alt="Solidabis cash">
            <img id="time" src="../assets/time.png" alt="Solidabis cash">
            <img id="nan" src="../assets/Nan.png" alt="Solidabis cash">
          </div>

          <div class="third">
            <p> Nopeus 2 (km/h) </p>
            <div class="number-input">
              <input id="speed_input_2" class="quantity" type="number" min="0"  value= "0" v-model="form.speed_input_2" @change="onChange($event)">
            </div>
            <div class="results" id="results_2">
              {{ (form.travel_input / 100 * (form.gas_button * 1.009 ** (form.speed_input_2))).toFixed(2) }}
            </div>
          </div>
        </div>

      </section>
    </div>
  </div>
</template>

<script>
export default {
  name: 'OispaBensaa',
  props: {
    msg: String
  },
  data: function () {
    return {
      form: {
        gas_button: '',
        travel_input: '',
        speed_input_1: '',
        speed_input_2: '',
      }
    };
  },
  methods: {
    onChange(event) {
      if(document.getElementById('car')) {
        document.getElementById('car').remove();
        document.getElementById('remove-style').remove();
      }
      var results_1 = parseFloat(document.getElementById("results_1").innerText);
      var results_2 = parseFloat(document.getElementById("results_2").innerText);
      console.log(results_1)
      console.log(results_2)

      var div = document.createElement('div');
      div.setAttribute("id", "car");
      var img = document.createElement('img');
      img.src = "/img/Solidabis_car.a95dd923.png";
      img.id = "remove-img";
      img.alt = "Solidabis car";
      img.style.width = "300px";
      img.style.height = "auto";

      // Create our stylesheet
      var style = document.createElement('style');
      style.id = "remove-style";
      style.innerHTML =
          "#car {top: 850px;position: absolute;-webkit-animation: linear;-webkit-animation-name: run;-webkit-animation-duration: 8s;}" +
          "@-webkit-keyframes run {0% {left: 0;}" +
          "48% {left: calc(40%);-webkit-transform: rotateY(0deg);}" +
          "50% {left: calc(40%); -webkit-transform: rotateY(180deg);}" +
          "60% {left: calc(40%);}" +
          "100% {left: -600px;-webkit-transform: rotateY(180deg);}";

      var ref = document.querySelector('script');

      if(results_1 < results_2) {
        document.getElementById("results_1").style.color = "#c9263f";
        document.getElementById("results_2").style.color = "black";
        document.getElementById("cash").style.display = "none";
        document.getElementById("time").style.display = "block";
        document.getElementById("nan").style.display = "none";

        document.getElementById('price').innerText = results_1.toFixed(2);
        document.getElementById('here').appendChild(div);
        document.getElementById('car').appendChild(img);
        ref.parentNode.insertBefore(style, ref);
        setTimeout(function(){
          if(document.getElementById('car')) {
            document.getElementById('car').remove();
            document.getElementById('remove-style').remove();
          }
        },8000);
      }else if (results_1 > results_2){
        document.getElementById("results_2").style.color = "#c9263f";
        document.getElementById("results_1").style.color = "black";
        document.getElementById("cash").style.display = "block";
        document.getElementById("time").style.display = "none";
        document.getElementById("nan").style.display = "none";
        document.getElementById('price').innerText = results_2.toFixed(2);
        document.getElementById('here').appendChild(div);
        document.getElementById('car').appendChild(img);
        ref.parentNode.insertBefore(style, ref);
        setTimeout(function(){
          if(document.getElementById('car')) {
            document.getElementById('car').remove();
            document.getElementById('remove-style').remove();
          }
        },8000);
      } else {
        document.getElementById("results_1").style.color = "black";
        document.getElementById("results_2").style.color = "black";
        document.getElementById("cash").style.display = "none";
        document.getElementById("time").style.display = "none";
        document.getElementById("nan").style.display = "block";
        document.getElementById('price').innerText = "NaN ";
      }
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  color: #c9263f;
}

.gas-container {
  display: flex;
  justify-content: space-between;
  flex-direction: row;
  max-width: 500px;
  margin: 0 auto;
}

.gas {
  padding: 10px;
  background-color: #c9263f;
  color: white;
  font-weight: bolder;
  margin: 20px;
  width: 100px;
}

.gas:hover {
  background-color: #9e2438;
  text-decoration: underline;

}

#cash, #time, #nan{
  display: none;
  margin-top: 60px;
  margin-left: auto;
  margin-right: auto;
  max-width: 200px;
  height: auto;
}
@media (max-width: 600px) {
  #cash, #time, #nan {
  max-width: 100px;
  }
}
#nan{
  display: block;
}

input[type=radio] {
  display: none;
}

input[type="radio"]:checked + label {
  background-color: #9e2438;
  text-decoration: underline;
}

h1 {
  margin-top: 10px;
  color: white;
  background-color: #c9263f;
  padding: 20px 0;
  width: 100%;
}

.speed-container {
  width: 80%;
  display: flex;
  flex-direction: row;
  margin: 0 auto;
}

.third {
  width: 33%;
}
input[type="number"] {
  -webkit-appearance: textfield;
  -moz-appearance: textfield;
  appearance: textfield;
}

input[type=number]::-webkit-inner-spin-button,
input[type=number]::-webkit-outer-spin-button {
  -webkit-appearance: none;
}

.number-input {
  border: 2px solid #c15d6e;
  display: inline-flex;
}

.number-input,
.number-input * {
  box-sizing: border-box;
}

.number-input button {
  outline:none;
  -webkit-appearance: none;
  background-color: transparent;
  border: none;
  align-items: center;
  justify-content: center;
  width: 2rem;
  height: 2rem;
  cursor: pointer;
  margin: 0;
  position: relative;
}

.number-input input[type=number] {
  font-family: sans-serif;
  max-width: 5rem;
  padding: .5rem;
  border: solid #ddd;
  border-width: 0 2px;
  font-size: 1.2rem;
  height: 3rem;
  font-weight: bold;
  text-align: center;
}

.results{
  margin-top: 30px;
  font-size: 2rem;
}

</style>
