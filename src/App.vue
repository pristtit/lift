<template>
<div class="working-window-mine">
  <div class="column" v-for="column of columns" :key="column">

      <columnMineBorder v-for="floor of floors" :key="floor"/>
      
      <cabin 
      :startParam="startParam"
      :nextColumn="nextColumn" 
      :column="column"
      :fakeQueue="fakeQueue"
      :arr="arr"
      :queue="queue"
      />
  </div>
  <div class="floorSideBar">
    <floorSideBar
    v-for="floor of floors"
    :key="floor"
    :floor="floor"
    :fakeQueue="fakeQueue"
    @pushListApp="pushListApp"
    :queue="queue"
    :arr="arr"
    />
  </div>
</div>
</template>

<script>
import columnMineBorder from "@/components/columnMineBorder"
import cabin from '@/components/cabin.vue'
import floorSideBar from '@/components/floorSideBar.vue'


export default {

  components: {
    cabin,
    floorSideBar,
    columnMineBorder,
  },

  data() {
    return {
      floors: 10,
      columns: 3,
      queue: [],
      fakeQueue: [],
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

          let listDistance = this.arr.map(function(item, index) { return {isActive: item.isActive, id: index, distance: Math.abs(this.nextFloor - item.floorNumber)}}, this);
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
        this.fakeQueue.push(floor);
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

.column {
  margin: 5px;
}

.floorSideBar {
  display: flex;
  flex-direction: column-reverse;
}
</style>
