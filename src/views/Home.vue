<template>
    <div class="home">
        <AddItem v-bind:shoppingItems="shoppingItems" v-on:add-item="addItem" />
        <ShoppingList
            v-bind:shoppingItems="shoppingItems"
            v-on:del-item="deleteItem"
            v-on:del-all="deleteAll"
        />
    </div>
</template>

<script>
import ShoppingList from "../components/ShoppingList.vue";
import AddItem from "../components/AddItem.vue";

export default {
    name: "Home",
    components: {
        ShoppingList,
        AddItem
    },
    data() {
        return {
            shoppingItems: []
        };
    },
    methods: {
        addItem(newItem) {
            localStorage.setItem(
                `shoppinglist.${newItem.id}`,
                JSON.stringify(newItem)
            );
            this.updateListArray();
        },
        deleteItem(id) {
            localStorage.removeItem(`shoppinglist.${id}`);
            this.updateListArray();
        },
        deleteAll() {
            this.shoppingItems.forEach(item => {
                if (item.done) {
                    localStorage.removeItem(`shoppinglist.${item.id}`);
                }
            });
            this.updateListArray();
        },
        updateListArray() {
            const prefix = /shoppinglist.*/;
            let storedItems = [];

            Object.keys(localStorage).forEach(key => {
                if (prefix.test(key)) {
                    let item = JSON.parse(localStorage.getItem(key));
                    storedItems.push(item);
                }
            });
            this.shoppingItems = storedItems;
        }
    },
    created() {
        this.updateListArray();
    }
};
</script>
