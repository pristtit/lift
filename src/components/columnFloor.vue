<template>
    <div class="column__floor">
        <columnMineBorder/>

        <div class="column__floor-sidebar">
            <columnBtnFloor 
            class="column__btn-floor column__btn-floor_display "
            @pushListApp="pushListApp"
            />

            <div class="column__number-floor">{{ floors + 1 - floor }}</div>
        </div>
    </div>
</template>

<script>
import columnMineBorder from "@/components/columnMineBorder"
import columnBtnFloor from "@/components/columnBtnFloor"

export default {

    components: {
        columnMineBorder,
        columnBtnFloor,
    },

    props: {
        floor: {
            type: Number,
        },
        floors: {
            type: Number,
        },
    },

    methods: {
        pushListApp() {
            this.$emit('pushListApp', this.floors + 1 - this.floor)
        }
    }
}
</script>

<style>

.column__floor {
    display: flex;
}

.column__number-floor {
    display: block;
    width: 20px;
}

.column__btn-floor_display {
    display: block;
    width: min-content;
}

</style>