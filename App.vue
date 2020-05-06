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
                v-bind:propsContent="note.content"
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
            notes: [
                {content: 'hardcoded content'},
                {content: 'hardcoded content'},
                {content: 'hardcoded content'}
            ]
        }
    },
    methods: {
        toggleView(){
            this.singleColumn = !this.singleColumn;
        },
        addNote(){
            this.notes.push({content: 'placeholder content'});
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