<template>
<div class="working-window-mine">
  <div class="column" v-for="column of columns" :key="column">
      <floor 
      v-for="floor of floors" 
      :floor="floor"
      :floors="floors"
      :column="column"
      :key="floor"
      @create="getList"
      />
      <cabin 
      :startParam="startParam"
      :chek="chek" 
      :column="column"
      :arr="arr"
      @cabineActive="cabineActive"
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
      arr.push({floorNumber: [1], isActive: true});
    }
    this.arr = arr;
  },

  data() {
    return {
      floors: 7,
      columns: 1,
      arr: null,
      chek: null,
      startParam: true,
    }
  },

  components: {
    floor,
    cabin,
  },

  methods: {
    getList(floor, column) {
      console.log(this.arr[0].isActive);
      let listDistance = this.arr.map(function(item, index) { return {isActive: item.isActive, id: index, distance: Math.abs(floor - item.floorNumber)}});
      listDistance.sort(function(a, b) { return a.distance - b.distance; });
      let minNumber = listDistance.find(item => item.isActive);
      if (minNumber) {
        this.arr[minNumber.id].floorNumber.push(floor);
        // this.arr[minNumber.id].isActive = false;
        this.chek = minNumber.id;
        this.startParam = !this.startParam;
      } else {
        this.arr[listDistance[0].id].floorNumber.push(floor);
        // this.arr[listDistance[0].id].isActive = false;
        this.chek = listDistance[0].id;
        this.startParam = !this.startParam;
      }  
    },
    cabineActive(column) {
      this.arr[column - 1].isActive = true;
      this.arr[column - 1].floorNumber.shift();
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
