<template>
    <input
      type="text"
      v-model="text"
      placeholder="Text"
      @keyup.enter="submit"
    />
    <button type="submit" @click="submit">Add</button>
    <ol>
        <li v-for="(todo, index) in todos">
            {{ todo }}
            <button @click="remove(index)">X</button>
        </li>
    </ol>
</template>

<script lang="ts">
import AtomButton from '@/components/atom/Button/AtomButton.vue';
import Text1 from '@/components/atom/Text/Text1.vue';
import { validate } from '@babel/types';
export default {
    data() {
        return {
            todos: [''],
            text: '',
        }
    },

    methods: {
        submit() {
            this.todos.push(this.text);
            this.text = '';
            
        },
        remove(index) { 
            this.todos.splice(index, 1);
        }
    }
}
</script>