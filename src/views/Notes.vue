<template>
    <div class="notes">
        <form v-on:submit.prevent="addNote">
            <textarea v-model="note" cols="40" rows="10"></textarea>
            <input type="submit" value="Save" class="btn" @click="$event.target.blur()" />
        </form>
        <div v-for="(note, index) in allNotes" v-bind:key="index">
            <div class="single-note">
                <p>{{note.content}}</p>
                <button class="del" @click="deleteNote(note.id)">X</button>
            </div>
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
            const id = uuidv4();
            const newNote = {
                id: id,
                content: this.note
            };
            localStorage.setItem(`notes.${id}`, JSON.stringify(newNote));
            this.updateNoteArray();
            this.note = "";
        },
        deleteNote(id) {
            localStorage.removeItem(`notes.${id}`);
            this.updateNoteArray();
        },
        updateNoteArray() {
            const prefix = /notes.*/;
            let storedNotes = [];

            Object.keys(localStorage).forEach(key => {
                if (prefix.test(key)) {
                    let item = JSON.parse(localStorage.getItem(key));
                    storedNotes.push(item);
                }
            });
            this.allNotes = storedNotes;
        }
    },
    created() {
        this.updateNoteArray();
    }
};
</script>

<style lang="scss">
.notes {
    margin-top: 10px;
    max-width: 600px;
    margin: 0 auto;
    padding: 10px;

    form {
        margin-bottom: 10px;

        input {
            display: block;
            margin: 0 auto;
        }
    }

    .single-note {
        background: rgb(244, 244, 244);
        padding: 10px;
        border-bottom: 1px #ccc dotted;
        display: flex;
        align-items: center;
        justify-content: flex-start;

        p {
            text-align: left;
            margin-right: 10%;
            white-space: pre-line;
        }
    }
}
</style>

