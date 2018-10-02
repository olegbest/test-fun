<template>
    <div id="app" class="app">
        <HelloWorld/>
    </div>
</template>

<script>
    import HelloWorld from './components/HelloWorld.vue'

    export default {
        name: 'app',
        components: {
            HelloWorld
        }
    }
</script>

<style>


    .app {
        height: 100%;
    }
</style>
