<template>
    <div id="app">
        <div id="nav">
            <router-link to="/">ShoppingList</router-link>
            <router-link to="/about">Notes</router-link>
        </div>
        <router-view />
    </div>
</template>

<style lang="scss">
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

#nav {
    padding: 30px;
    background: #333;
    border-bottom: 5px #97b5d3 solid;

    a {
        font-weight: bold;
        color: #97b5d3;
        text-decoration: none;
        padding: 10px;
        margin: 0 10px;

        &.router-link-exact-active {
            background: #97b5d3;
            color: #333;
            border-radius: 5px;
        }
    }
}

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
}

.btn {
    display: inline-block;
    border: none;
    background: #3d4d5e;
    color: #fff;
    padding: 7px 20px;
    cursor: pointer;
    border-radius: 1px;
}

.btn:hover {
    background: #4a5c70;
}
</style>
