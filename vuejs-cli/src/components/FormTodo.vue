<template>
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
</template>

<script>
    export default {
        data() {
            return { 
                name: "",
                message: ""
            }
        },
        methods: {            
            addComment() {
                this.$emit("add-todo", {
                    name: this.name,
                    message: this.message
                })

                this.name = ""
                this.message = ""
            }
        }
    }
</script>