<template>
<div class="working-window-mine">
  <div class="column" v-for="column of columns" :key="column">
      <floor 
      v-for="floor of floors" 
      :floor="floor"
      :column="column"
      :key="floor"
      @create="getList"
      />
      <cabin 
      :chek="chek" 
      :column="column"
      :arr="arr"
      />
  </div>
</div>
</template>

<script>
import floor from "@/components/floor"
import cabin from '@/components/cabin.vue'

export default {

  mounted() {
    let arr = [];
    for (let a = 0; a < this.columns; a++) {
      arr.push({floorNumber: [1], freeState: true});
    }
    this.arr = arr;
  },

  data() {
    return {
      floors: 5,
      columns: 2,
      arr: null,
      chek: null,
    }
  },

  components: {
    floor,
    cabin,
  },

  methods: {
    getList(floor, column) {
      let listDistance = this.arr.map(function(item, index) { return {freeState: item.freeState, id: index, distance: Math.abs(floor - item.floorNumber)}});
      listDistance.sort(function(a, b) { return a.distance - b.distance; });
      let minNumber = listDistance.find(item => item.freeState);
      if (minNumber) {
        this.arr[minNumber.id].floorNumber.push(floor);
        this.arr[minNumber.id].floorNumber.shift();
        this.arr[minNumber.id].freeState = false;
        this.chek = minNumber.id;
        // console.log(this.chek);
        // console.log(this.arr);
      } else {
        this.arr[listDistance[0].id].floorNumber.push(floor);
        this.arr[listDistance[0].id].floorNumber.shift();
        this.arr[listDistance[0].id].freeState = false;
        this.chek = listDistance[0].id;
        // console.log(this.chek);
        // console.log(this.arr);
      }  
    }
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
