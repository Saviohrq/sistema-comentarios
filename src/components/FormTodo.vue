<script setup>
import { ref } from 'vue';

const name = ref('');
const message = ref('');

const emit = defineEmits(['add-todo']);

function addComment() {
    if (message.value.trim() === '') {
        name.value = '';
        return;
    }
    
    emit('add-todo', {
        name: name.value,
        message: message.value
    });

    name.value = '';
    message.value = '';
}
</script>

<template>
    <div class="form-todo form-group">
        <p>
            <input placeholder="Nome" type="text" name="author" v-model="name">
        </p>
        <p>
            <textarea placeholder="Comentário" name="message" class="form-control" v-model="message"></textarea>
        </p>
        <button @click="addComment" type="submit" class="btn btn-primary">Comentar</button>
    </div>
</template>