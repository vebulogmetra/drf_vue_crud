<template>

<div>
<form class="form-horizontal" @submit="submitForm" id="mainf"></form>
<div class="form-group">
    <div class="col-3"></div><label class="form-label">Title</label>
    <div class="col-9"></div><input form="mainf" class="form-input" type="text" v-model="title" placeholder="Type note title..." />
</div>
<div class="form-group">
    <div class="col-3"></div><label class="form-label">Body</label>
    <div class="col-9"></div><textarea form="mainf" class="form-input" v-model="body" rows="8" placeholder="Type your note..."></textarea>
</div>
<div class="form-group">
    <div class="col-3"></div>
    <div class="col-9"></div><button form="mainf" class="btn btn-primary" type="submit">Create</button>
</div>
</div>


</template>


<script>
export default {
    name: 'create-note',
    data () {
    return {
        'title': '',
        'body': ''
    }
    },
    methods: {
    submitForm (event) {
        this.createNote()
        // Т.к. мы уже отправили запрос на создание заметки строчкой выше,
        // нам нужно теперь очистить поля title и body
        this.title = ''
        this.body = ''
        // preventDefault нужно для того, чтобы страница
        // не перезагружалась после нажатия кнопки submit
        event.preventDefault()
    },
    createNote () {
        // Вызываем действие `createNote` из хранилища, которое
        // отправит запрос на создание новой заметки к нашему API.
        this.$store.dispatch('createNote', { title: this.title, body: this.body })
    }
    }
}
</script>