<template>
    <div id="app">
        <Header/>
        <main>
            <MoviesContainer/>
        </main>
    </div>
</template>

<script>
import Header from './components/Header.vue'
import MoviesContainer from './components/MoviesContainer.vue'

export default {
    name: 'App',
    components: {
      Header,
      MoviesContainer
    }
}
</script>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
}

* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}
</style>
