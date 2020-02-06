<template>
    <div id="app">
        <div id="dashboard-wrapper">
            <Dashboard/>
        </div>
    </div>
</template>
<script>
    import Dashboard from './components/Dashboard';

    export default {
        name: 'app',
        components: {
            Dashboard
        },
        data: () => ({}),
        mounted() {
        },
        methods: {},
    }
</script>
<style>
    html {
        font-size: .5rem;
    }

    #app {
        font-family: 'Avenir', Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    #dashboard-wrapper {
    }
</style>
