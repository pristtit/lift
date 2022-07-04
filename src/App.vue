<template>
<div v-for="floor in floors" class="app">
  <floor/>
</div>
</template>

<script>
import floor from "@/components/floor"
export default {
  data() {
    return {
      floors: [1,2,3],
    }
  },
  components: {
    floor,
  }
}
</script>

<style>

* {
	padding: 0;
	margin: 0;
	border: 0;
}

.app {
  padding-left: 10px
}
</style>
