<template>
  <Notes
    @selected-note="selectedNote"
    @upd-note="updateNote"
    @delete-note="deleteNote"
    @add-note="createNote"
    :notes="notes"
  />
</template>

<script>
import Notes from "../components/notes/Notes.vue"
import Button from "../components/Button.vue"
export default {
  name: "NoteView",
  components: {
    Notes,
    Button,
  },
  data() {
    return {
      notes: [],
      selectedNoteId: "",
    }
  },
  methods: {
    selectedNote(id) {
      this.selectedNoteId = id
    },
    async updateNote(note) {
      const noteUpdated = {
        title: note.title,
        description: note.description,
      }
      const res = await fetch(
        `https://62a7032797b6156bff84ef49.mockapi.io/api/notes/${this.selectedNoteId}`,
        {
          method: "PUT",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(noteUpdated),
        }
      )
      const data = await res.json()

      this.notes = this.notes.map((note) =>
        note.id === this.selectedNoteId
          ? { ...note, title: data.title, description: data.description }
          : note
      )
    },
    async createNote(note) {
      const res = await fetch(
        "https://62a7032797b6156bff84ef49.mockapi.io/api/notes",
        {
          method: "POST",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(note),
        }
      )
      const data = await res.json()

      this.notes = [...this.notes, data]
    },
    async deleteNote(id) {
      if (confirm("Sure?")) {
        const res = await fetch(
          `https://62a7032797b6156bff84ef49.mockapi.io/api/notes/${id}`,
          {
            method: "DELETE",
          }
        )
        res.status === 200
          ? (this.notes = this.notes.filter((note) => note.id !== id))
          : alert("Error!")
      }
    },
    async fetchNotes() {
      const res = await fetch(
        "https://62a7032797b6156bff84ef49.mockapi.io/api/notes"
      )
      const data = await res.json()

      return data
    },
  },
  async created() {
    this.notes = await this.fetchNotes()
  },
}
</script>

<style>
.cus-btn {
  text-transform: uppercase;
}
</style>
