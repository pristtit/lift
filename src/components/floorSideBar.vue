<template>
  <div class="floorSideBar">
    <sideBarBtnFloor
    :floor="floor"
    :fakeQueue="fakeQueue"
    @pushListApp="pushListApp"
    />

    <div class="floorSideBar__numberFloor">{{ floor }}</div>
  </div>
</template>

<script>
import sideBarBtnFloor from "@/components/sideBarBtnFloor"

export default {

    components: {
        sideBarBtnFloor,
    },

    props: {
        floor: {
            type: Number,
        },
        fakeQueue: {
            type: Array
        },
    },

    methods: {
        pushListApp() {
            this.$emit('pushListApp', this.floor)
        }
    }
}
</script>

<style>

.floorSideBar__numberFloor {
    display: block;
    width: 20px;
    text-align: center
}

.floorSideBar {
    height: 50px;
    position: relative;
    bottom: 50px;
}
</style>