<template>
  <div class="wrapper">
    <Navbar @setSearch="searchValue = $event" />
    <Notes @editNote="editNote" @delNote="delNote" :notes="filterNotes" />
    <Modal :edit="edit" @addNote="addNote" @send="modalShow = $event" @close="modalShow = !modalShow"
      :modalShow="modalShow" v-show="!modalShow" :editedNote="editedNote" @newNote="newNote" />
    <button @click="modalShow = !modalShow, edit = true" class="modal__show_btn"><img src="@/assets/images/edit.svg"
        alt=""></button>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';
import Navbar from './components/Navbar.vue';
import Notes from './components/Notes.vue';

export default {
  components: { Navbar, Notes, Modal },
  data() {
    return {
      notes: [],

      modalShow: true,
      edit: true,
      editedNote: null,
      searchValue: '',
    }
  },
  computed: {

    filterNotes() {

      /*  return this.notes.filter( note => note.title.includes(this.searchValue)) */
      return this.searchValue ? this.notes.filter(note => note.title.toLowerCase().includes(this.searchValue.toLowerCase())) : this.notes

    }


  },

  mounted() {
    this.getNotes()
  },
  methods: {
    addNote(note) {

      this.notes.push(note)


    },
    getNotes() {

      let localNotes = localStorage.notes
      if (localNotes) {
        this.notes = JSON.parse(localNotes)
      }


    },

    delNote(id) {
      let index = this.notes.findIndex((note) => note.id == id)
      this.notes.splice(index, 1)
    },
    editNote(id) {
      this.modalShow = this.edit = false
      let currenNote = this.notes.find(note => note.id == id)
      this.editedNote = currenNote


    },
    newNote(newEditedNote) {

      this.notes.forEach(note => {
        if (note.id == newEditedNote.id) {
          note.title = newEditedNote.title
          note.text = newEditedNote.text
          note.data = newEditedNote.data


        }


      })

    }
  },

  watch: {
    notes: {

      handler() {
        localStorage.notes = JSON.stringify(this.notes)


      },
      deep: true

    }
  },
}
</script>

