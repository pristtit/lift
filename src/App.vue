<template>
<div class="workingWindowMine">
  <div class="column" v-for="column of columns" :key="column">

      <mineBorder v-for="floor of floors" :key="floor"/>
      
      <cabin 
      :commonNextFloor="commonNextFloor"
      :startParam="startParam"
      :nextColumn="nextColumn" 
      :column="column"
      :fakeQueue="fakeQueue"
      :arr="arr"
      :queue="queue"
      />
  </div>

  <div class="divFloorSideBar">
    <floorSideBar
    v-for="floor of floors"
    :key="floor"
    :floor="floor"
    :fakeQueue="fakeQueue"
    @pushListApp="pushListApp"
    />
  </div>
</div>
</template>

<script>
import mineBorder from "@/components/mineBorder"
import cabin from '@/components/cabin.vue'
import floorSideBar from '@/components/floorSideBar.vue'


export default {

  components: {
    cabin,
    floorSideBar,
    mineBorder,
  },

  data() {
    return {
      floors: 7,
      columns: 3,
      queue: [],
      fakeQueue: [],
      arr: [],
      nextColumn: undefined,
      commonNextFloor: [],
      startParam: true,
    }
  },

  mounted() {
    
    // this.queue = JSON.parse(sessionStorage.getItem("queue")) || []
    // this.fakeQueue = JSON.parse(sessionStorage.getItem("fakeQueue")) || []
    // this.nextColumn = JSON.parse(sessionStorage.getItem("nextColumn")) || null
    // this.nextFloor = JSON.parse(sessionStorage.getItem("appNextFloor")) || null
    // this.startParam = JSON.parse(sessionStorage.getItem("startParam")) || true
    

    // if (JSON.parse(sessionStorage.getItem("arr"))) {
    //   this.arr = JSON.parse(sessionStorage.getItem("arr"));
    // } else {
    //   this.arr = [];
    //   for (let columnIter = 0; columnIter < this.columns; columnIter++) {
    //     this.arr.push({floorNumber: 1, isActive: false});
    //   }
    // }
    for (let columnIter = 0; columnIter < this.columns; columnIter++) {
        this.arr.push({floorNumber: 1, isActive: false, index: columnIter});
    }
    
    // setInterval(() => {
    //   if (this.queue.length > 0) {
    //     if (this.arr.find(item => item.isActive === false)) {

    //       let listDistance = this.arr.map(function(item, index) { return {isActive: item.isActive, id: index, distance: Math.abs(this.nextFloor - item.floorNumber)}}, this);
    //       listDistance.sort(function(a, b) { return a.distance - b.distance });

    //       this.nextColumn = listDistance.find(item => !item.isActive).id;
    //       this.arr[this.nextColumn].isActive = true;
    //       this.startParam = !this.startParam;
    //     }
    //   }
    // }, 30);
  },
  
  watch: {
    queue: {
      handler() {
        if (this.arr.find(item => !item.isActive) && this.commonNextFloor.length > 0) {
          let listDistance = this.arr.map(function(item, index) { return {isActive: item.isActive, id: index, distance: Math.abs(this.commonNextFloor[0] - item.floorNumber)}}, this);
          listDistance.sort(function(a, b) { return a.distance - b.distance });

          this.nextColumn = listDistance.find(item => !item.isActive).id;
          this.arr[this.nextColumn].isActive = true;
          this.startParam = !this.startParam;
          }
      },
      deep: true
    }

  //   queue: {
  //     handler(newValue) {
  //       console.log('o');
  //       sessionStorage.setItem("queue", JSON.stringify(newValue));
  //     },
  //     deep: true
  //   },

  //   fakeQueue: {
  //     handler(newValue) {
  //       console.log('f');
  //       sessionStorage.setItem("fakeQueue", JSON.stringify(newValue));
  //     },
  //     deep: true
  //   },

  //   nextColumn(newValue) {
  //     sessionStorage.setItem("nextColumn", JSON.stringify(newValue));
  //   },

  //   nextFloor(newValue) {
  //     sessionStorage.setItem("appNextFloor", JSON.stringify(newValue));
  //   },

  //   startParam(newValue) {
  //     sessionStorage.setItem("startParam", JSON.stringify(newValue));
  //   },

  //   arr: {
  //     handler(newValue) {
  //       sessionStorage.setItem("arr", JSON.stringify(newValue));
  //     },
  //     deep: true
  //   },
  },

  methods: {
    pushListApp(floor) {
      if (!this.queue.includes(floor) && !this.arr.find(element => element.floorNumber === floor)) {
        this.commonNextFloor.push(floor);
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

.workingWindowMine {
  display: flex;
  height: 90vh;
  width: 90vw;
  justify-content: left;
  align-items: flex-end;
  padding: 0 5% 0 5%;
}

.column {
  display: flex;
  flex-direction: column;
  align-content: center;
  margin: 5px;
}

.divFloorSideBar {
  display: flex;
  flex-direction: column-reverse;
}
</style>
