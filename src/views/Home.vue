<template>
    <div class="home">
        <AddItem v-on:add-item="addItem" />
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
            // const { item, completed } = newItem;
            // this.shoppingItems = [...this.shoppingItems, newItem];
            localStorage.setItem(
                `shoppinglist.${newItem.name}`,
                JSON.stringify(newItem)
            );
            this.shoppingItems.push(newItem);
        },
        deleteItem(name, index) {
            localStorage.removeItem(`shoppinglist.${name}`);
            this.shoppingItems.splice(index, 1);
        },
        deleteAll() {
            this.shoppingItems.forEach((item, index) => {
                if (item.done) {
                    localStorage.removeItem(`shoppinglist.${item.name}`);
                    this.shoppingItems.splice(index, 1);
                }
            });
        }
    },
    created() {
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
};
</script>
