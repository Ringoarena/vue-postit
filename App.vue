<template>
<div class="wrapper">
    <header>
        <button
            v-on:click="toggleView"
        >L/C</button>
        <button
            v-on:click="addNote"
        >Add Note</button>
    </header>
    <main>
        <section class="postit-container" v-bind:class="{listView: singleColumn}">
            <postit
                v-bind:key="index"
                v-for="(note, index) in notes"
                v-bind:propsId="note.id"
                v-bind:propsContent="note.content"
                v-on:submitEvent="submitEventHandler"
                v-on:deleteEvent="deleteEventHandler"
            />
        </section>
    </main>
</div>
</template>

<script>
import Postit from './Postit'

export default {
    name: 'App',
    components: {
        postit: Postit
    },
    data(){
        return {
            singleColumn: false,
            idCounter: 1,
            notes: []
        }
    },
    methods: {
        toggleView(){
            this.singleColumn = !this.singleColumn;
        },
        addNote(){
            this.notes.push({id: this.idCounter++, content: 'placeholder content'});
        },
        submitEventHandler(payload){
            let foundNote = this.notes.find(note => note.id == payload.id);
            foundNote.content = payload.data;
        },
        deleteEventHandler(payload){
            // let indexToDelete = this.notes.findIndex(note => note.id == payload.id);
            // this.notes.splice(indexToDelete, 1);
            this.notes = this.notes.filter(note => note.id != payload.id);
        }
    }
}
</script>

<style>
header {
    border-bottom: 2px solid black;
}
.postit-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
    /* background-color: rgb(216, 216, 216); */
    margin-top: 1rem;
}

.listView {
    grid-template-columns: repeat(1, 1fr);
}
</style>