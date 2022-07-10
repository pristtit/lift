<template>
  <div class="column__floor-sidebar">
    <columnBtnFloor
    :floor="floor"
    :fakeQueue="fakeQueue"
    @pushListApp="pushListApp"
    />

    <div class="column__number-floor">{{ floor }}</div>
  </div>
</template>

<script>
import columnBtnFloor from "@/components/columnBtnFloor"

export default {

    components: {
        columnBtnFloor,
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

.column__number-floor {
    display: block;
    width: 20px;
    text-align: center
}

.column__floor-sidebar {
    height: 50px;
    position: relative;
    bottom: 50px;
}
</style>