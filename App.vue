<template>
<div class="wrapper">
    <header>
        <div class="buttons">
        <button
            v-on:click="toggleView"
        >List / Column</button>
        <button
            v-on:click="addNote"
        >Add Note</button>
        </div>
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
            this.notes.push({id: this.idCounter++, content: 'hardcoded content'});
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
    border-bottom: 5px solid black;
    padding-bottom: 0.5rem;
}

.buttons{
    max-width: 1024px;
    margin: 0 auto;
}
.postit-container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 1rem;
    max-width: 1024px;
    margin: 1rem auto 0 auto;
}

.listView {
    grid-template-columns: repeat(1, 1fr);
}
</style>