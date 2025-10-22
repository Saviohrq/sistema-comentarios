<script setup>
import  FormTodo  from './FormTodo.vue';
import { ref, computed, watch } from 'vue';

const comments = ref([]);

function addComment(comment) {
    comments.value.push(comment);
}

function removeComment(index) {
    comments.value.splice(index, 1);
}

const allComments = computed(() => {
    return comments.value.map(comment => ({
        ...comment,
        name: comment.name.trim() === '' ? 'Anônimo' : comment.name
    }))
});

watch(comments, (val) => {
    console.log('val', val)
}, {
    deep: true
});

</script>

<template>
    <div class="container">
        <h1>Comentários</h1>
        <hr />
        <FormTodo @add-todo="addComment"></FormTodo>
        <div class="list-group">
            <div class="list-group-item" v-for="(comment, index) in allComments">
                <span class="comment_author">Autor: <strong>{{ comment.name }}</strong></span>
                <p>{{ comment.message }}</p>
                <div>
                    <a href="#" title="excluir" @click.prevent="removeComment(index)">Excluir</a>
                </div>
            </div>
        </div>
        <hr />
    </div>
</template>