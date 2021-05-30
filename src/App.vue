<template>
  <div id="app">
    <Animation/>
    <OispaBensaa msg="Oispa bensaa huoltoasema"/>
    <Ascii price="45,50"/>
    <div id="icons">
      <a href="https://www.linkedin.com/in/roosa-virta/" target="_blank">
        <font-awesome-icon class="linkedin" :icon="['fab', 'linkedin']" />
      </a>
      <a href="https://github.com/ThistleFIN" target="_blank">
        <img id="github_img" src="./assets/thistlefin.png" alt="ThistleFIN - Github">
      </a>
    </div>
  </div>
</template>

<script>
import OispaBensaa from './components/OispaBensaa.vue'
import Ascii from './components/Ascii.vue'
import Animation from './components/Animation.vue'


export default {
  name: 'App',
  components: {
    OispaBensaa,
    Ascii,
    Animation
  }
}
</script>

<style>
html, body{
  margin: 0 !important;
  width: 100% !important;
  height: 100% !important;
}
body{
  background-color: #f5f1eb;
  font-family: "Segoe UI",Tahoma,Geneva,Verdana,sans-serif;
}
#icons{
  position: fixed;
  left: 20px;
  bottom: 20px;
}
.linkedin{
  font-size: 3em;
  color: #c9263f;
}

#github_img{
  margin-left: 10px;
  height: 3em;
  width: auto;
  color: #c9263f;
}
#github_img:hover{
  filter: brightness(80%);
}

.linkedin:hover{
  color: #9e2438;
}

#app {
  text-align: center;
}

.wrap{
  max-width: 1200px;
  height: 520px;
  margin: 0 auto;
}

.row {
  margin-top: 56px;
  background-color: #fff;
  width: 100%;
}
</style>
