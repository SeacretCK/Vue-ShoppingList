<template>
    <div>
        <form v-on:submit.prevent="addItem">
            <input type="text" v-model="itemInput" placeholder="Add a new Item..." />
            <input type="submit" value="Add" class="btn" @click="$event.target.blur()" />
        </form>
    </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
    name: "AddItem",
    props: ["shoppingItems"],
    data() {
        return {
            itemInput: ""
        };
    },
    methods: {
        addItem() {
            const newItem = {
                id: uuidv4(),
                name: this.itemInput,
                done: false
            };
            this.$emit("add-item", newItem);
            this.itemInput = "";
        }
    }
};
</script>


<style lang="scss" scoped>
div {
    max-width: 600px;
    margin: 0 auto;

    form {
        display: flex;
        justify-content: flex-start;

        input[type="text"] {
            padding: 15px;
            width: 100%;
        }

        input[type="submit"] {
            margin-left: auto;
        }
    }
}
</style>