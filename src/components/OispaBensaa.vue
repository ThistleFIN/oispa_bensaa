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
      if(document.getElementById('stop')) {
        document.getElementById('stop').remove();
        document.getElementById('remove-cat-style').remove();
      }
      var results_1 = parseFloat(document.getElementById("results_1").innerText);
      var results_2 = parseFloat(document.getElementById("results_2").innerText);
      var speed_1 = parseFloat(document.getElementById("speed_input_1").value);
      var speed_2 = parseFloat(document.getElementById("speed_input_2").value);
      console.log((speed_1))
      console.log((speed_2))
      //car animation
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

      //Epsu animation
      var div2 = document.createElement('div');
      div2.setAttribute("id", "stop");
      var img2 = document.createElement('img');
      img2.src = "data:image/png;base64,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";
      img2.id = "stop_img";
      img2.alt = "Stop!";

      // Create our stylesheet
      var style2 = document.createElement('style');
      style2.id = "remove-cat-style";
      style2.innerHTML =
          "#stop_img { position: absolute;top: 750px;-webkit-animation: linear;-webkit-animation-name: run2;-webkit-animation-duration: 8s;}"+
          "@-webkit-keyframes run2 {"+
          "0% {right: 0;} 15% {right: calc(20% - 100px);}"+
          "48% {right: calc(20% - 100px);} 50% {right: calc(20% - 100px);}"+
          "55%{right: calc(30% - 100px);}"+
          "100% {right: 110%;} };"

      var ref2 = document.querySelector('script');

      if( speed_1 > 0 && speed_2 > 0 && results_1 < results_2) {
        document.getElementById("results_1").style.color = "#c9263f";
        document.getElementById("results_2").style.color = "black";
        document.getElementById("cash").style.display = "none";
        document.getElementById("time").style.display = "block";
        document.getElementById("nan").style.display = "none";

        document.getElementById('price').innerText = results_1.toFixed(2);
        document.getElementById('here').appendChild(div);
        document.getElementById('car').appendChild(img);

        ref.parentNode.insertBefore(style, ref);
        if(speed_1 > 120 || speed_2 > 120){
          document.getElementById('here2').appendChild(div2);
          document.getElementById('stop').appendChild(img2);
          ref2.parentNode.insertBefore(style2, ref2);
        }
        setTimeout(function(){
          if(document.getElementById('car')) {
            document.getElementById('car').remove();
            document.getElementById('remove-style').remove();
          }
          if(document.getElementById('stop')) {
            document.getElementById('stop').remove();
            document.getElementById('remove-cat-style').remove();
          }
        },8000);
      }else if ( speed_1 > 0 && speed_2 > 0 && results_1 > results_2){
        document.getElementById("results_2").style.color = "#c9263f";
        document.getElementById("results_1").style.color = "black";
        document.getElementById("cash").style.display = "block";
        document.getElementById("time").style.display = "none";
        document.getElementById("nan").style.display = "none";
        document.getElementById('price').innerText = results_2.toFixed(2);
        document.getElementById('here').appendChild(div);
        document.getElementById('car').appendChild(img);
        ref.parentNode.insertBefore(style, ref);
        if(speed_1 > 120 || speed_2 > 120){
          document.getElementById('here2').appendChild(div2);
          document.getElementById('stop').appendChild(img2);
          ref2.parentNode.insertBefore(style2, ref2);
        }
        setTimeout(function(){
          if(document.getElementById('car')) {
            document.getElementById('car').remove();
            document.getElementById('remove-style').remove();
          }
          if(document.getElementById('stop')) {
            document.getElementById('stop').remove();
            document.getElementById('remove-cat-style').remove();
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
