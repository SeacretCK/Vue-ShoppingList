<template>
    <div>
        <form v-on:submit.prevent="addItem">
            <input type="text" v-model="itemInput" placeholder="Add a new Item..." />
            <input type="submit" value="Submit" class="btn" />
        </form>
    </div>
</template>

<script>
export default {
    name: "AddItem",
    data() {
        return {
            itemInput: ""
        };
    },
    methods: {
        addItem() {
            const newItem = {
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

        input[type="text"] {
            flex: 10;
            padding: 5px;
        }

        input[type="submit"] {
            flex: 2;
        }
    }
}
</style>