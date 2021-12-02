<template>
    <header>
        <div id="logo">
            Boolflix
        </div>

        <div id="search">
            <input v-model="stringToSearch" @focus="stringToSearch = ''" type="text" placeholder="scrivi qui cosa vuoi cercare...">
            <button @click="$emit('searchString', stringToSearch)">Cerca</button>
        </div>
    </header>
</template>

<script>
export default {
    name: 'Header',
    data() {
        return {
            stringToSearch: ""
        }
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">

header {
    background-color: black;
    height: 80px;
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 0 30px;

    #logo {
        font-size: 30px;
        color: red;
    }

    #search {

        input {
            width: 200px;
            margin: 0 10px;
        }

        button {
            padding: 0 5px;
        }
    }
}
</style>
