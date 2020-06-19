<template>
  <div>
    <div class="level two">
      <h1>{{ftbelow}} ft Below Sea Level</h1>
      <p id="l_r_2" class="level_reached">In Component 2<br />this.go = {{this.go}}<br />this.go_three = {{go_three}}</p>
      <p id="r_2" class="reset">$emit('reset');</p>
    </div>
    <LevelThree :ftbelow="ftbelow + 500" :beacon_count="beacon_count" :go_three="go_three" @reset="reset"></LevelThree>
  </div>
</template>

<script>
import LevelThree from './LevelThree.vue';

export default {
  name: 'LevelTwo',
  props: {
    ftbelow: Number,
    beacon_count: Number,
    go: Boolean
  },
  data: function() {
    return {
      go_three : false
    }
  },
  watch: {
    go: async function(newVal) {
      if(newVal) {
        document.getElementById('l_r_2').classList.add('show');
        let c = document.getElementById('thecircle');
        let delay = 0;
        for(let bottom = 0; bottom >= -100; bottom -= 1.02) {
          window.setTimeout(function() {
             c.style.bottom = bottom + '%';
           }, delay);
           delay += 75;
        }
        await (new Promise(res => setTimeout(res, delay)));
        document.getElementById('l_r_2').classList.remove('show');
        this.go_three = true;
        // window.clearTimeout(to_id);
      }
    }
  },
  methods: {
    reset: function() {
      let reset_p = document.getElementById('r_2');
      window.setTimeout(function() {
        reset_p.classList.add('show');
      }, 2000);
      this.go_three = false;
      this.$emit('reset');
      window.setTimeout(function() {
        reset_p.classList.remove('show');
      }, 3000);
    }
  },
  components: {
    LevelThree
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>

</style>
