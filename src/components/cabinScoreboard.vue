<template>
  <div v-show="this.arr[this.column - 1]?.isActive" class="cabin__scoreboard cabin__scoreboard_size">
    <div 
    :class="{cabin__direction_up: draw, cabin__direction_down: !draw}"
    class="cabin__direction"></div>

    <div class="cabin__numberFloor">{{ nextFloor }}</div>
  </div>
</template>

<script>
export default {

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
    draw: {
      type: Boolean
    }
  },

}
</script>

<style>

.cabin__scoreboard {
  background-color: rgba(150, 144, 144, 0.692);
  border-radius: 2px;
  display: flex;
  justify-content: center;
}

.cabin__scoreboard_size {
  width: 40px;
  height: 20px;
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

.cabin__numberFloor {
  display: flex;
  justify-content: center;
  width: 20px;
  height: 20px;
}
</style>