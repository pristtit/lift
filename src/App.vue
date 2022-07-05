<template>
<div class="working-window-mine">
  <div class="column" v-for="column of columns" :key="column">
      <floor v-for="floor of floors" :key="floor"/>
      <cabin/>
  </div>
</div>
</template>

<script>
import floor from "@/components/floor"
import cabin from '@/components/cabin.vue'
export default {
  data() {
    return {
      floors: 5,
      columns: 2,
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

.working-window-mine {
  display: flex;
  height: 100vh;
  width: 100vw;
  justify-content: left;
  align-items: flex-end;
  padding: 0 5% 0 5%;
}

</style>
