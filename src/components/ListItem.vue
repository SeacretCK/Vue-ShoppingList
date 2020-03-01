<template>
    <div>
        <div class="list-item">
            <input type="checkbox" name="item.name" :checked="item.done" v-on:change="markDone" />
            <div @click="editItem(item)">
                <p v-bind:class="{'is-done':item.done}">{{item.name}}</p>
            </div>

            <button class="del" @click="$emit('del-item', item.id)">X</button>
        </div>
        <form class="edit-item" v-if="editMode">
            <input class="edit-input" type="text" v-model="editInput" />
            <button class="edit-btn" @click="saveEditedItem(item)">Save</button>
        </form>
    </div>
</template>

<script>
export default {
    name: "ListItem",
    props: ["item"], // = the value of each iteration in ShoppingList
    data() {
        return {
            editMode: false,
            editInput: ""
        };
    },
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
        },
        editItem() {
            this.editMode = true;
            this.editInput = this.item.name;
        },
        saveEditedItem() {
            localStorage.setItem(
                `shoppinglist.${this.item.id}`,
                JSON.stringify({
                    id: this.item.id,
                    name: this.editInput,
                    done: this.item.done
                })
            );
            this.$emit("update-list");
            this.editMode = false;
            this.editInput = "";
        }
    }
};
</script>

<style lang="scss">
.list-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
    display: flex;
    align-items: center;
    justify-content: flex-start;

    .is-done {
        text-decoration: line-through;
    }

    input[type="checkbox"] {
        padding: 20px;
        margin-right: 20px;
        margin-left: 10px;
    }

    div {
        width: 100%;

        p {
            text-align: left;
            margin-right: 10%;
        }
    }
}

.edit-item {
    padding: 10px;
    display: flex;
    justify-content: flex-start;

    .edit-btn {
        background: #658d4a;
        color: #fff;
        border: none;
        padding: 10px;
        border-radius: 1px;
        cursor: pointer;
        margin-left: auto;
        margin-right: 10px;
    }

    .edit-input {
        width: 100%;
        padding: 10px;
        margin-left: 10px;
    }
}
</style>