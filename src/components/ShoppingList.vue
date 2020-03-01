<template>
    <div>
        <h3>ShoppingList</h3>
        <div class="shopping-list" v-for="(item, index) in shoppingItems" v-bind:key="index">
            <ListItem
                v-bind:item="item"
                v-bind:index="index"
                v-on:del-item="$emit('del-item', item.name, index)"
            />
        </div>
        <button class="btn" @click="$emit('del-all')">Delete Checked</button>
    </div>
</template>

<script>
import ListItem from "./ListItem.vue";

export default {
    name: "ShoppingList",
    components: {
        ListItem
    },
    props: ["shoppingItems"]
};
</script>

<style scoped>
h3 {
    padding: 20px;
}
.shopping-list {
    max-width: 600px;
    margin: 0 auto;
}
.btn {
    margin-top: 20px;
}
</style>