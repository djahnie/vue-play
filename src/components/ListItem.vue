<template>
    <div>
        <div v-if="isEdited">
            <input v-model="textToEdit" />
            <button @click="submitEditedText">Submit</button>
        </div>
        <div v-else>
            {{ title }}
            <button @click="editTodo">Edit</button>
            <button @click="deleteTodo">Delete</button>
        </div>
    </div>
</template>

<script>
export default {
    props: [ 'title' ],
    data: function() {
        return {
            isEdited: false,
            textToEdit: ''
        }
    },
    methods: {
        editTodo: function () {
            console.log("I want to edit!")
            this.isEdited = true
            this.textToEdit = this.title
        },
        submitEditedText: function () {
            this.$emit('textEdited', this.textToEdit) // we create an event that is called 'textEdited' and emit two parameters
            this.isEdited = false
        },
        deleteTodo: function() {
            this.$emit('itemDeleted', this.title)
        }
    }
}
</script>

        // splice basically means remove a part from an array
        // the position is the first argument and the count the second
        // so it means 'remove this one item'



           // this.$emit('delete', this.title)
