<template>
  <div v-show="this.arr[this.column - 1]?.isActive" class="cabin__scoreboard">
    <div 
    :class="{cabin__direction_up: draw, cabin__direction_down: !draw}"
    class="cabin__direction"></div>
    <div class="cabin__number-floor">{{ nextFloor }}</div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      q: false,
      w: false,
    }
  },

  props: {
    nextFloor: {
      type: Number
    },
    arr: {
      type: Array
    },
    column: {
      type: Number
    },
    x: {
      type: Number
    },
    draw: {
      type: Boolean
    }
  },

  computed: {
    go() {
      th
    }
  }
}
</script>

<style>

.cabin__scoreboard {
    display: flex;
    height: 40px;
    width: 40px;
}

.cabin__direction {

  width: 20px;
  height: 20px;
}

.cabin__direction_up {
  background-image: url(@/assets/up.png);
  background-size: cover;
}

.cabin__direction_down {
  background-image: url(@/assets/down.png);
  background-size: cover;
}

.cabin__number-floor {
  width: 20px;
  height: 20px;
}
</style>