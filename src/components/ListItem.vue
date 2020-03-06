<template>
    <div>
        <div class="list-item" v-if="!editMode">
            <div id="container-checkbox">
                <input type="checkbox" name="item.name" :checked="item.done" v-on:change="markDone" />
                <label for="item.name">
                    <div></div>
                </label>
            </div>
            <div id="container-list-item" @click="editItem(item)">
                <p v-bind:class="{'is-done':item.done}">{{item.name}}</p>
            </div>

            <button class="del" @click="$emit('del-item', item.id)">X</button>
        </div>
        <form class="edit-item" v-if="editMode">
            <input
                class="edit-input"
                type="text"
                v-model="editInput"
                @blur="saveEditedItem(item)"
                ref="edit"
            />
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
            this.$nextTick(() => this.$refs.edit.focus());
            // Vue.nextTick( [callback, context] ) - Defer the callback to be executed after the next DOM update cycle. Use it immediately after you’ve changed some data to wait for the DOM update.
            // without it the element couldn't be grabbed and returned undefined
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
        padding: 30px;
        margin-right: 10px;
        margin-left: 10px;
    }

    #container-list-item {
        width: 100%;
        margin-left: 30px;

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

#container-checkbox {
    margin: 0 auto;
    display: block;
    width: 25px;
    height: 25px;
    border: solid 1px rgba(0, 0, 10, 0.4);
    border-radius: 5px;
    position: relative;
    background: #97b5d3;

    & label {
        height: 25px;
        width: 25px;
        z-index: 0;
        display: inline-block;
        position: absolute;
        top: 0;
        left: 0;
    }

    & input {
        height: 25px;
        width: 25px;
        margin: 0;
        opacity: 0;
        z-index: 1;
        position: relative;
        cursor: pointer;

        &:checked + label > div {
            border-radius: 0;
            border: 2px solid #3d4d5e;
            border-top: 0;
            border-left: 0;
            height: 18px;
            width: 9px;
            margin-left: 7px;
            transform: rotate(40deg);

            transition: opacity 150ms ease-in-out;
        }
    }
}
</style>