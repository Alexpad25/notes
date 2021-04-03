<template>
  <div class="wrapper">

    <header></header>

    <div class="wrapper-content">
      <section>
        <div class="container">

          <message v-if="message" :message="message" />

          <!-- new-note -->
          <newNote :note="note" @addNote="addNote" />

          <div class="note-header">
            <h1> {{ title }} </h1>

            <!-- search -->
            <search
                :value="search"
                placeholder="Поиск поста"
                @search="search = $event"/>

            <!-- icons controls -->
            <div class="icon">
              <svg :class="{ active: grid }" @click="grid = true" version="1.1" id="Layer_1" xmlns="http://www.w3.org/2000/svg" xmlns:xlink="http://www.w3.org/1999/xlink" x="0px" y="0px" viewBox="0 0 512 512" style="enable-background:new 0 0 512 512;" xml:space="preserve"><g><path d="M187.628,0H43.707C19.607,0,0,19.607,0,43.707v143.921c0,24.1,19.607,43.707,43.707,43.707h143.921 c24.1,0,43.707-19.607,43.707-43.707V43.707C231.335,19.607,211.728,0,187.628,0z"/><path d="M468.293,0H324.372c-24.1,0-43.707,19.607-43.707,43.707v143.921c0,24.1,19.607,43.707,43.707,43.707h143.921c24.1,0,43.707-19.607,43.707-43.707V43.707C512,19.607,492.393,0,468.293,0z"/><path d="M187.628,280.665H43.707C19.607,280.665,0,300.272,0,324.372v143.921C0,492.393,19.607,512,43.707,512h143.921c24.1,0,43.707-19.607,43.707-43.707V324.372C231.335,300.272,211.728,280.665,187.628,280.665z"/><path d="M468.293,280.665H324.372c-24.1,0-43.707,19.607-43.707,43.707v143.921c0,24.1,19.607,43.707,43.707,43.707h143.921c24.1,0,43.707-19.607,43.707-43.707V324.372C512,300.272,492.393,280.665,468.293,280.665z"/></g></svg>
              <svg :class="{ active: !grid }" @click="grid = false" enable-background="new 0 0 24 24" height="512" viewBox="0 0 24 24" width="512" xmlns="http://www.w3.org/2000/svg"><path d="m5 0h-4c-.552 0-1 .448-1 1v4c0 .552.448 1 1 1h4c.552 0 1-.448 1-1v-4c0-.552-.448-1-1-1z"/><path d="m23 0h-14c-.552 0-1 .448-1 1v4c0 .552.448 1 1 1h14c.552 0 1-.448 1-1v-4c0-.552-.448-1-1-1z"/><path d="m5 9h-4c-.552 0-1 .448-1 1v4c0 .552.448 1 1 1h4c.552 0 1-.448 1-1v-4c0-.552-.448-1-1-1z"/><path d="m23 9h-14c-.552 0-1 .448-1 1v4c0 .552.448 1 1 1h14c.552 0 1-.448 1-1v-4c0-.552-.448-1-1-1z"/><path d="m5 18h-4c-.552 0-1 .448-1 1v4c0 .552.448 1 1 1h4c.552 0 1-.448 1-1v-4c0-.552-.448-1-1-1z"/><path d="m23 18h-14c-.552 0-1 .448-1 1v4c0 .552.448 1 1 1h14c.552 0 1-.448 1-1v-4c0-.552-.448-1-1-1z"/></svg>
            </div>
          </div>

          <!-- Note list -->
          <note :notes="notesFilter" :grid="grid" @remove="removeNote" />

        </div>
      </section>
    </div>

    <footer></footer>

  </div>
</template>

<script>

import message from "./components/Message";
import newNote from "./components/NewNote";
import note from "./components/Note";
import search from "./components/Search";

export default {
  components: {
    newNote,
    message,
    note,
    search
  },
  data () {
    return {
      title: 'Note App',
      grid: true,
      search: '',
      message: null,
      note: {
        title: '',
        descr: '',
      },
      notes: [
        {title: 'First', descr: 'Description for first note', date: new Date(Date.now()).toLocaleString() },
        {title: 'Second', descr: 'Description for second note', date: new Date(Date.now()).toLocaleString() },
        {title: 'Third', descr: 'Description for third note', date: new Date(Date.now()).toLocaleString() }
      ]
    }
  },
  computed: {
    notesFilter () {
      let array = this.notes,
          search = this.search
      if (!search) return array
      search = search.trim().toLowerCase()
      // Filter
      array = array.filter(function (item) {
        if (item.title.toLowerCase().indexOf(search) !== -1) {
          return item
        }
      })
      // Error
        return array
    }
  },
  methods: {
    addNote() {
      let {title, descr} = this.note;

      if(title === '') {
        this.message = 'Title can`t empty!'
        return false
      }

      this.notes.push({
            title: title,
            descr: descr,
            date: new Date(Date.now()).toLocaleString(),
          }
      );

      this.message = null
      this.note.title = ''
      this.note.descr = ''

      console.log(this.notes)
    },
    removeNote(id) {
      this.notes.splice(id, 1)
    }
  }
}
</script>

<style lang="scss">
</style>