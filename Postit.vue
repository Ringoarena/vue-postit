<template>
<article>
    <button
        v-on:click="toggleEditMode"
        v-bind:class="{hidden: editMode}"
    >Edit</button>
    <button
        v-on:click="fireDeleteEvent"
        v-bind:class="{hidden: editMode}"
    >Delete</button>
    <button
        v-on:click="fireSubmitEvent"
        v-bind:class="{hidden: !editMode}"
    >Submit</button>
    <input 
        type="text"
        v-bind:class="{hidden: !editMode}"
        v-model="newContent"
    >
    <select name="colors" v-bind:class="{hidden: !editMode}">
        <option value="black">Black</option>
        <option value="red">Red</option>
        <option value="blue">Blue</option>
    </select>
    <p>id: {{propsId}}</p>
    <p
        v-bind:class="{hidden: editMode}">
        {{propsContent}}
    </p>
</article>
</template>

<script>
export default {
    props: {
        propsId: Number,
        propsContent: String
    },
    data(){
        return {
            editMode: false,
            newContent: ''
        }
    },
    methods: {
        toggleEditMode(){
            this.editMode = !this.editMode;
        },
        fireSubmitEvent(){
            this.$emit('submitEvent', {id: this.propsId, data: this.newContent});
            this.toggleEditMode();
        },
        fireDeleteEvent(){
            this.$emit('deleteEvent', {id: this.propsId});
        }
    }
}
</script>

<style>
article{
    border: 1px solid black;
    padding: 0.5rem;
}

.hidden{
    display: none;
}

</style>