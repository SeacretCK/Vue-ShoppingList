<template>
    <div class="list-item">
        <input type="checkbox" v-on:change="markDone" />
        <p v-bind:class="{'is-done':item.done}">{{item.name}}</p>
        <button class="del" @click="$emit('del-item', item.name, index)">X</button>
    </div>
</template>

<script>
export default {
    name: "ListItem",
    props: ["item", "index"], // = the value of each iteration in ShoppingList
    methods: {
        markDone() {
            this.item.done = !this.item.done;
            localStorage.setItem(
                `shoppinglist.${this.item.name}`,
                JSON.stringify({
                    name: this.item.name,
                    done: this.item.done
                })
            );
        }
    }
};
</script>

<style>
.list-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
    display: flex;
    align-items: center;
    justify-content: flex-start;
}
.is-done {
    text-decoration: line-through;
}
.del {
    background: #ff0000;
    color: #fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    margin-left: auto;
}
input[type="checkbox"] {
    padding: 10px;
    margin-right: 20px;
}
</style>