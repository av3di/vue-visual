<template>
  <div id="app">
    <div class="level">
      <h1>Sea Level ({{ftbelow}} ft below)</h1>
      <div id="thecircle" class="circle pulsating"></div>
      <p id="r_1" class="reset">this.go = false;<br />Reset event recieved!</p>
      <button v-if="!go" @click="dropBeacon">Drop Beacon</button>
    </div>
    <LevelTwo :ftbelow="ftbelow + 500" :beacon_count="beacon_count" :go="go" @reset="reset"></LevelTwo>
  </div>
</template>

<script>
import LevelTwo from './components/LevelTwo.vue';

export default {
  name: 'App',
  data: function() {
      return {
        ftbelow: 0,
        beacon_count: 0,
        go: false
      }
  },
  components: {
    LevelTwo
  },
  methods: {
    async dropBeacon() {
      this.beacon_count++;
      let c = document.getElementById('thecircle');
      let delay = 500;
      for(let bottom = 50; bottom > 0; bottom--) {
        window.setTimeout(function() {
           c.style.bottom = bottom + 'px';
         }, delay);
         delay += 75;
      }
      await (new Promise(res => setTimeout(res, delay)));
      this.go = true;
      // window.clearTimeout(to_id);
    },
    async reset() {
      let reset_p = document.getElementById('r_1');
      window.setTimeout(function() {
        reset_p.classList.add('show');
      }, 3000);
      window.setTimeout(function() {
        reset_p.classList.remove('show');
        let c = document.getElementById('thecircle');
        c.style.opacity = 1;
      }, 6000);
      await (new Promise(res => setTimeout(res, 6000)));
      this.go = false;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  position: relative;
  text-align: center;
  color: #FFFFFF;
}
button {
  border: solid 2px #FFFFFF;
  border-radius: 2px;
  background-color: rgba(255, 255, 255, 0);
  color: #FFFFFF;
  padding: 7px 10px;
  position: absolute;
  right: 25px;
  bottom: 25px;
  font-weight: bold;
  font-size: 16px;
  -webkit-transition: all 0.25s ease-in-out;
  -moz-transition: all 0.25s ease-in-out;
  -ms-transition: all 0.25s ease-in-out;
  transition: all 0.25s ease-in-out;
}
button:focus {
  outline: 0px;
}
button:hover {
  border: solid 2px rgb(234, 107, 107);
  color: rgb(234, 107, 107);
  cursor: pointer;
  -webkit-transition: all 0.25s ease-in-out;
  -moz-transition: all 0.25s ease-in-out;
  -ms-transition: all 0.25s ease-in-out;
  transition: all 0.25s ease-in-out;
}
h1 {
  font-size: 18px;
}
.level {
  background: rgba(2, 64, 89, 0.2);
  padding-top: 25px;
  width: 100%;
  min-height: 135px;
  position: relative;
}
.level.two {
  background: rgba(2, 64, 89, 0.4);
}
.level.three {
  background: rgba(2, 64, 89, 0.6);
}
.level.four {
  background: rgba(2, 64, 89, 0.8);
}
p.counter {
  position: absolute;
  bottom: 25px;
  width: 100%;
  text-align: center;
}
p.level_reached {
  margin-top: 20px;
  text-align: left;
  padding-left: 15px;
  opacity: 0;
  transition: all 1s ease-in-out;
}
p.level_reached.show {
  opacity: 1;
  transform: translate(0px, -15px);
  transition: all 1s ease-in-out;
}
p.reset {
  text-align: right;
  padding-right: 15px;
  opacity: 0;
  transition: all 1s ease-in-out;
}
p.reset.show {
  opacity: 1;
  transform: translate(0px, -30px);
  transition: all 1s ease-in-out;
}
.circle {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background-color: rgb(242, 7, 7);
  box-shadow: 0px 0px 10px 5px rgba(242, 7, 7, 1);
  position: absolute;
  margin-left: auto;
  margin-right: auto;
  left: 0;
  right: 0;
  bottom: 50px;
}
.roll {
  -webkit-transform: translateX(-20px);
  -ms-transform: translateX(-20px);
  transform: translateX(-20px);
  transition: all 2s ease-out;
}
.pulsating {
  -webkit-animation: pulse 3s infinite ease-in-out;
  -moz-animation: pulse 3s infinite ease-in-out;
  animation: pulse 3s infinite ease-in-out;
}
@keyframes pulse {
  0% {
    background-color: rgb(242, 7, 7);
    box-shadow: 0px 0px 10px 5px rgba(242, 7, 7, 1);
  }
  50% {
    background-color: rgb(179, 5, 5);
    box-shadow: 0px 0px 10px 5px rgba(242, 7, 7, 0.4);
  }
  100% {
    background-color: rgb(242, 7, 7);
    box-shadow: 0px 0px 10px 5px rgba(242, 7, 7, 1);
  }
}
</style>
