<template>
    <div id="app">
        <div class="container">
            <h1>Comentários</h1>
            <hr>
            <div class="form-todo form-group">
                <p>
                    <input type="text" placeholder="Nome" class="form-control" v-model="name">
                </p>
                <p>
                    <textarea placeholder="Comentário" class="form-control" v-model="message"></textarea>
                </p>
                <button class="btn btn-info" v-on:click="addComment">Comentar</button>
                <hr>
            </div>
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
export default {
    data() {
        return { 
            comments: [],
            name: "",
            message: ""
        }
    },
    methods: {
        addComment() {
            if(this.name.trim() != "" || this.message.trim() != ""){
                this.comments.push({
                    name: this.name,
                    message: this.message
                })
                this.name = ""
                this.message = ""
            }
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
    },
    watch: {
        comments(comments) {
            console.log(comments)
        }
    }
}
</script>