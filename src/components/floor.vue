<template>
    <div class="floor">
        <mine/>
        <btnLift/>
        <div class="numberFloor">5</div>
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

.floor {
    width: 100px;
    height: 50px;
    min-width: 50px;
    min-height: 50px;
}

.numberFloor {
    display: inline-block;
    position: relative;
    bottom: 10px;
    left: -10px;
}
</style>