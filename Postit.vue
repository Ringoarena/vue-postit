<template>
<article>
    <button v-on:click="toggleEditMode">Edit</button>
    <input type="text" v-bind:class="{hidden: !editMode}" v-model="newContent">
    <p v-bind:class="{hidden: editMode}">{{propsContent}}</p>
</article>
</template>

<script>
export default {
    props: {
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
        fireEditEvent(){
            this.$emit('editEvent', this.newContent);
        }
    }

}
</script>

<style>
article{
    border: 1px solid black;
}

.hidden{
    display: none;
}

</style>