<template>
<article>
    <button
        v-on:click="toggleEditMode"
        >Edit
    </button>
    <button
        v-on:click="fireSubmitEvent"
        >Submit
    </button>
    
    <input 
        type="text"
        v-bind:class="{hidden: !editMode}"
        v-model="newContent"
    >
    <p>{{propsId}}</p>
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