<template>
  <div class="level four">
    <h1>{{ ftbelow }} ft Below Sea Level</h1>
    <p id="l_r_4" class="level_reached">In Component 4<br />this.go_four = {{go_four}}</p>
    <p id="r_4" class="reset">$emit('reset');</p>
    <button v-if="this.beacon_floor" @click="resetBeacon">Reset Beacon</button>
    <p class="counter">Beacons dropped: {{ beacon_count }}</p>
  </div>
</template>

<script>
export default {
  name: 'LevelFour',
  props: {
    ftbelow: Number,
    beacon_count: Number,
    go_four: Boolean
  },
  data: function() {
    return {
      beacon_floor : false
    }
  },
  watch: {
    go_four: async function(newVal) {
      if(newVal) {
        document.getElementById('l_r_4').classList.add('show');
        let c = document.getElementById('thecircle');
        let delay = 0;
        for(let bottom = -201; bottom >= -300; bottom -= 1.75) {
          window.setTimeout(function() {
             c.style.bottom = bottom + '%';
           }, delay);
           delay += 75;
        }
        await (new Promise(res => setTimeout(res, delay)));
        document.getElementById('l_r_4').classList.remove('show');
        c.classList.add('roll');
        this.beacon_floor = true;
        // window.clearTimeout(to_id);
      }
    }
  },
  methods: {
    resetBeacon: function() {
      let c = document.getElementById('thecircle');
      c.style.opacity = 0;
      c.style.bottom = '50px';
      c.classList.remove('roll');
      this.beacon_floor = false;
      let reset_p = document.getElementById('r_4');
      reset_p.classList.add('show');
      this.$emit('reset');
      window.setTimeout(function() {
        reset_p.classList.remove('show');
      }, 1000);
    }
  }
}
</script>
