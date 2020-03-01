<template>
    <div class="notes">
        <form v-on:submit.prevent="addNote">
            <textarea v-model="note" cols="40" rows="10"></textarea>
            <input type="submit" value="Save" class="btn" />
        </form>
        <div>
            <p></p>
        </div>
    </div>
</template>

<script>
import { v4 as uuidv4 } from "uuid";

export default {
    name: "Notes",
    data() {
        return {
            note: "",
            allNotes: []
        };
    },
    methods: {
        addNote() {
            const newNote = this.note;
            const id = uuidv4();
            localStorage.setItem(`notes.${id}`, newNote);
            this.allNotes.push(newNote);
        }
    }
};
</script>

<style lang="scss" scoped>
.notes {
    margin-top: 10px;

    form input {
        display: block;
        margin: 0 auto;
    }
}
</style>