<template>
<div class="working-window-mine">
  <div class="column" v-for="column of columns" :key="column">

      <columnFloor 
      v-for="floor of floors" 
      :floor="floor"
      :floors="floors"
      :key="floor"
      @pushListApp="pushListApp"
      />
      
      <cabin 
      :startParam="startParam"
      :nextColumn="nextColumn" 
      :column="column"
      :arr="arr"
      :nextFloor="nextFloor"
      :queue="queue"
      />
  </div>
</div>
</template>

<script>
import columnFloor from "@/components/columnFloor"
import cabin from '@/components/cabin.vue'

export default {

  components: {
    columnFloor,
    cabin,
  },

  data() {
    return {
      floors: 7,
      columns: 3,
      queue: [],
      arr: [],
      nextColumn: null,
      nextFloor: null,
      startParam: true,
    }
  },

  mounted() {
    
    for (let columnIter = 0; columnIter < this.columns; columnIter++) {
      this.arr.push({floorNumber: 1, isActive: false});
    }

    setInterval(() => {
      if (this.queue.length > 0) {
        if (this.arr.find(item => item.isActive === false)) {

          let listDistance = this.arr.map(function(item, index) { return {isActive: item.isActive, id: index, distance: Math.abs(this.flor - item.floorNumber)}}, this);
          listDistance.sort(function(a, b) { return a.distance - b.distance });

          this.nextColumn = listDistance.find(item => !item.isActive).id;
          this.arr[this.nextColumn].isActive = true;
          this.startParam = !this.startParam;
        }
      }
    }, 30);
  },

  methods: {
    pushListApp(floor) {
      this.nextFloor = floor;

      if (!this.queue.includes(floor) && !this.arr.find(element => element.floorNumber === floor)) {
        this.queue.push(floor);
      }
    },
  }
}
</script>

<style>

* {
	padding: 0;
	margin: 0;
	border: 0;
}

.working-window-mine {
  display: flex;
  height: 100vh;
  width: 100vw;
  justify-content: left;
  align-items: flex-end;
  padding: 0 5% 0 5%;
}

</style>
