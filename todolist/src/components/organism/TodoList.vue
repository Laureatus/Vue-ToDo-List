<template>
    <input
      type="text"
      v-model="text"
      placeholder="Text"
      @keyup.enter="submit"
    />
    <div v-if="isEditing">
        <button type="submit" @click="update">Update</button>
    </div>
    <div v-else>
        <button type="submit" @click="submit">Add</button>
    </div>
    
    <ol>
        <li v-for="(todo, index) in todos">
            {{ todo }}
            <button @click="edit(index, todo)">Edit</button>
            <button @click="remove(index)">X</button>
        </li>
    </ol>
    <button @click="toggleDeleted">Show deleted ToDo's</button>
    <div v-if="showDeleted">
        <ol>
            <li v-for="done in finished">
                {{ done }}
            </li>
        </ol>
    </div>
</template>

<script lang="ts">
export default {
    data() {
        return {
            selectedIndex: null,
            todos: [],
            finished: ['Test', 'Done'],
            text: '',
            isEditing: false,
            showDeleted: false,
        }
    },

    methods: {
        submit() {
            this.todos.push(this.text);
            this.text = '';
        },
        remove(index) { 
            let deleted = this.todos[index];
            this.todos.splice(index, 1);
            this.finished.push(deleted);
        },
        edit(index, todo) {
            this.text = todo;
            this.selectedIndex = index;
            this.isEditing = true;
        },
        update() {
            this.todos.splice(this.selectedIndex, 1, this.text);
            this.isEditing = false;
         },
        toggleDeleted() {
            if (this.showDeleted == true) {
                this.showDeleted = false;
            } else {
                this.showDeleted = true;
            }
        },
    }
}
</script>
<style>

</style>