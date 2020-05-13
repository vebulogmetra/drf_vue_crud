<template>
<div>
<div class="card" v-for="note in notes" v-bind:key="note.title">
    <div class="card-header"></div><button class="btn btn-clear float-right" @click="deleteNote(note)"></button>
    <div class="card-title">{{ note.title }}</div>
    <div class="card-subtitle">{{ note.created_at }}</div>
    <div class="card-body">{{ note.body }}</div>
</div>
</div>
</template>


<script>
import { mapGetters } from 'vuex'
export default {
    name: 'note-list',
    computed: mapGetters(['notes']),
    methods: {
    deleteNote (note) {
        // Вызываем действие `deleteNote` из нашего хранилища, которое
        // попытается удалить заметку из нашех базы данных, отправив запрос к API
        this.$store.dispatch('deleteNote', note)
    }
    },
    beforeMount () {
    // Перед тем как загрузить страницу, нам нужно получить список всех
    // имеющихся заметок. Для этого мы вызываем действие `getNotes` из
    // нашего хранилища
    this.$store.dispatch('getNotes')
    }
}
</script>
<style>
    header {
    margin-top: 50px;
    }
</style>