<template>
    <div class="column__floor">
        <mine/>
        <div class="column__floor-sidebar">
            <btnLift class="column__btn-floor column__btn-floor_display "/>
            <div class="column__number-floor">5</div>
        </div>
    </div>
</template>

<script>
import mine from "@/components/mine"
import btnLift from "@/components/btnLift"
export default {
    components: {
        mine,
        btnLift,
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
    width: 20px;
}

</style>