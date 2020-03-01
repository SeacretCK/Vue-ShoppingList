<template>
    <div>
        <h3 v-if="shoppingItems.length == 0">Create a ShoppingList</h3>
        <h3 v-else>Things to buy</h3>
        <div class="shopping-list" v-for="(item, index) in shoppingItems" v-bind:key="index">
            <ListItem v-bind:item="item" v-on:del-item="$emit('del-item', item.id)" />
        </div>
        <button v-if="shoppingItems.length > 0" class="btn" @click="$emit('del-all')">Delete Checked</button>
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
    color: #3d4d5e;
}
.shopping-list {
    max-width: 600px;
    margin: 0 auto;
}
.btn {
    margin-top: 20px;
}
</style>