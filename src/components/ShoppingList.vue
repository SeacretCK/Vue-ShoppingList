<template>
    <div>
        <h3 v-if="shoppingItems.length == 0">Create a ShoppingList</h3>
        <h3 v-else>Things to buy</h3>
        <div class="shopping-list" v-for="(item, index) in shoppingItems" v-bind:key="index">
            <ListItem
                v-bind:item="item"
                v-on:del-item="$emit('del-item', item.id)"
                v-on:update-list="$emit('update-list')"
            />
        </div>
        <button
            v-if="shoppingItems.length > 0 && !allChecked"
            class="btn"
            @click="$emit('check-all'); $event.target.blur()"
        >Check All</button>
        <button
            v-if="shoppingItems.length > 0 && allChecked"
            class="btn"
            @click="$emit('uncheck-all'); $event.target.blur()"
        >Uncheck All</button>
        <button
            v-if="shoppingItems.length > 0"
            class="btn"
            @click="$emit('del-all'); $event.target.blur()"
        >Delete Checked</button>
    </div>
</template>

<script>
import ListItem from "./ListItem.vue";

export default {
    name: "ShoppingList",
    components: {
        ListItem
    },
    props: ["shoppingItems"],
    computed: {
        allChecked() {
            let count = 0;
            this.shoppingItems.forEach(item => {
                if (item.done) {
                    count++;
                }
            });
            return count === this.shoppingItems.length; // true when all checked
        }
    }
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