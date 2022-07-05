<template>
    <butten @click="pushListApp">жми</butten>
</template>

<script>
export default {
    methods: {
        pushListApp() {
            this.$emit('create')
        }
    }
    
}
</script>

<style>

.column__btn-floor {
    background-color: blue;
}
</style>