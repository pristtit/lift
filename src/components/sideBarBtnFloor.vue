<template>
    <butten
    :class="{floorSidebar__btnOn: fakeQueue.includes(floor)}"
    class="floorSidebar__btn-floor"
    @click="pushListApp"
    >
    </butten>
</template>

<script>
export default {

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
            this.$emit('pushListApp')
        }
    },
    
}
</script>

<style>

.floorSidebar__btn-floor {
    background-image: url(@/assets/btnFloor.png);
    background-size: contain;
    display: block;
    width: 20px;
    height: 20px;
}

.floorSidebar__btnOn {
    background-color: rgb(140, 255, 0);
}
</style>