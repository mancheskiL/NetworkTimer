<template>
    <div class="container">
        <input id='input'>
        <button v-on:click="submit">Submit</button>
        <button v-on:click="clear">Clear</button>
    </div>
</template>

<script>
// import Input from './Input.vue'

export default {
    name: 'Container',
    methods: {
        submit() {
            // pass
        },
        clear() {
            // pass
        }
    }
}
</script>

<style scoped>
    button {
        padding: 10px
    }
</style>