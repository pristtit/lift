<template>
<div class="deepMine">
  <div v-for="floor in floors" :key="floor" class="app">
    <floor/>
  </div>
  <cabin/>
</div>
</template>

<script>
import floor from "@/components/floor"
import cabin from '@/components/cabin.vue'
export default {
  data() {
    return {
      floors: [1,2,3],
    }
  },
  components: {
    floor,
    cabin,
  }
}
</script>

<style>

* {
	padding: 0;
	margin: 0;
	border: 0;
}

.deepMine {
  display: inline-block;
  padding-left: 10px
}
</style>
