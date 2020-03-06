<template>
    <div id="app">
        <div id="nav">
            <router-link to="/">ShoppingList</router-link>
            <router-link to="/notes">SimpleNotes</router-link>
        </div>
        <router-view />
    </div>
</template>

<style lang="scss">
$primary-color-dark: #333;
$primary-color-light: #97b5d3;
$button-color: #3d4d5e;
$button-hover: #4a5c70;

* {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
}

body {
    font-family: Arial, Helvetica, sans-serif;
    line-height: 1.4;
}

#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
}

#nav {
    padding: 30px;
    background: $primary-color-dark;
    border-bottom: 12px $primary-color-light solid;

    a {
        font-weight: bold;
        color: $primary-color-light;
        text-decoration: none;
        padding: 10px;
        margin: 0 10px;

        &.router-link-exact-active {
            background: $primary-color-light;
            color: $primary-color-dark;
            border-radius: 5px;
        }
    }
}

.btn {
    display: inline-block;
    border: none;
    background: $button-color;
    color: #fff;
    padding: 10px 20px;
    cursor: pointer;
    border-radius: 1px;

    .btn:hover {
        background: $button-hover;
    }
}

.del {
    background: #8d4a4a;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    margin-left: auto;
}
</style>
