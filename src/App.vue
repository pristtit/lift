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
      <cabin/>
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
      arr.push([1]);
    }
    this.arr = arr;
  },
  data() {
    return {
      floors: 5,
      columns: 2,
      arr: null,
    }
  },
  components: {
    floor,
    cabin,
  },
  methods: {
    getList(floor, column) {
      this.arr[column-1].push(floor);
      this.arr[column-1].shift();
      console.log(this.arr);
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
