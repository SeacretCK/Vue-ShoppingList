<template>
    <div class="list-item">
        <input type="checkbox" name="item.name" :checked="item.done" v-on:change="markDone" />
        <p v-bind:class="{'is-done':item.done}">{{item.name}}</p>
        <button class="del" @click="$emit('del-item', item.id)">X</button>
    </div>
</template>

<script>
export default {
    name: "ListItem",
    props: ["item"], // = the value of each iteration in ShoppingList
    methods: {
        markDone() {
            this.item.done = !this.item.done;
            localStorage.setItem(
                `shoppinglist.${this.item.id}`,
                JSON.stringify({
                    id: this.item.id,
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
    background: #8d4a4a;
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