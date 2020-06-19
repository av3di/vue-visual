<template>
  <div>
    <div class="level three">
      <h1>{{ ftbelow }} ft Below Sea Level</h1>
      <p id="l_r_3" class="level_reached">In Component 3<br />this.go_three = {{go_three}}<br />this.go_four = {{ go_four }}</p>
      <p id="r_3" class="reset">$emit('reset');</p>
    </div>
    <LevelFour :ftbelow="ftbelow + 500" :beacon_count="beacon_count" :go_four="go_four" @reset="reset"></LevelFour>
  </div>
</template>

<script>
import LevelFour from './LevelFour.vue';

export default {
  name: 'LevelThree',
  props: {
    ftbelow: Number,
    beacon_count: Number,
    go_three: Boolean
  },
  data: function() {
    return {
      go_four : false
    }
  },
  watch: {
    go_three: async function(newVal) {
      if(newVal) {
        document.getElementById('l_r_3').classList.add('show');
        let c = document.getElementById('thecircle');
        let delay = 0;
        for(let bottom = -101; bottom >= -200; bottom-= 1.15) {
          window.setTimeout(function() {
             c.style.bottom = bottom + '%';
           }, delay);
           delay += 75;
        }
        await (new Promise(res => setTimeout(res, delay)));
        document.getElementById('l_r_3').classList.remove('show');
        this.go_four = true;
        // window.clearTimeout(to_id);
      }
    }
  },
  methods: {
    reset: function() {
      let reset_p = document.getElementById('r_3');
      window.setTimeout(function() {
        reset_p.classList.add('show');
      }, 1000);
      this.go_four = false;
      this.$emit('reset');
      window.setTimeout(function() {
        reset_p.classList.remove('show');
      }, 2000);
    }
  },
  components: {
    LevelFour
  }
}
</script>
