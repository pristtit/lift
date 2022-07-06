<template>
    <div class="column__floor">
        <mine/>
        <div class="column__floor-sidebar">
            <btnLift 
            class="column__btn-floor column__btn-floor_display "
            @create="pushListApp"
            />
            <div class="column__number-floor">{{ 6 - floor }}</div>
        </div>
    </div>
</template>

<script>
import mine from "@/components/mine"
import btnLift from "@/components/btnLift"
export default {
    data() {
        return {
            actived: true,
        }
    },
    props: {
        floor: {
            type: Number,
        },
        floors: {
            type: Number,
        },
        column: {
            type: Number,
        }
    },
    components: {
        mine,
        btnLift,
    },
    methods: {
        pushListApp() {
            this.$emit('create', this.floors + 1 - this.floor, this.column)
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