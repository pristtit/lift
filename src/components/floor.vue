<template>
    <div class="floor">
        <mine/>
        <btnLift/>
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
    width: 50px;
    height: 50px;
    min-width: 50px;
    min-height: 50px;
}
</style>