<template>
    <div id="app">
        <div class="container">
            <h1>Comentários</h1>
            <hr>

            <FormTodo v-on:add-todo="addComment"></FormTodo>
            
            <div class="list-group">
                <div class="list-group-item" v-for="(comment, index) in allComments" :key="index">
                    <span class="comment__author">Author: <strong>{{comment.name}}</strong></span>
                    <span><p>{{comment.message}}</p></span>
                    <div>
                        <a href="#" title="Excluir" v-on:click.prevent="removeComment(index)">Excluir</a>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import FormTodo from './FormTodo'

export default {
    components: {
        FormTodo
    },
    data() {
        return { 
            comments: [],
            name: "",
            message: ""
        }
    },
    methods: {
        addComment(comment) {
            this.comments.push(comment)
        },
        removeComment(index) {
            this.comments.splice(index, 1)
        }
    },
    computed: {
        allComments() {
            return this.comments.map(comment=>({
                ...comment,
                name: comment.name.trim() === "" ? "Anônimo" : comment.name,
                message: comment.message.trim() == "" ? "Sem mensagem." : comment.message
            }))
        }
    }
}
</script>