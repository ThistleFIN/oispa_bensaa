<template>
  <div id="pot">
    <img id="car_img" src="../assets/Solidabis_car.png" alt="Solidabis car">
  </div>
</template>

<script>
export default {
  name: "Animation"
}
</script>

<style scoped>
img{
  max-height: 40px;
  width: auto;
}
#pot {
  top: 15px;
  position: absolute;
  -webkit-animation: linear infinite;
  -webkit-animation-name: run;
  -webkit-animation-duration: 10s;
}
@-webkit-keyframes run {
  0% {
    left: 0;
  }
  48% {
    -webkit-transform: rotateY(0deg);
  }
  50% {
    left: calc(100% - 127px);
    -webkit-transform: rotateY(180deg);
  }
  98% {
    -webkit-transform: rotateY(180deg);
  }
  100% {
    left: 0;
    -webkit-transform: rotateY(0deg);
  }
}
</style>