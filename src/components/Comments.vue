<script setup>
import { ref, computed, watch } from 'vue';

const comments = ref([]);
const name = ref('');
const message = ref('');

function addComment() {
    if (message.value.trim() === '') {
        name.value = '';
        return;
    }
    comments.value.push({
        name: name.value,
        message: message.value
    });

    name.value = '';
    message.value = '';
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
        <div class="form-todo form-group">
            <p>
                <input placeholder="Nome" type="text" name="author" v-model="name">
            </p>
            <p>
                <textarea placeholder="Comentário" name="message" class="form-control" v-model="message"></textarea>
            </p>
            <button @click="addComment" type="submit" class="btn btn-primary">Comentar</button>
        </div>
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