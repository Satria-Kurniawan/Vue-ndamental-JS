<template>
  <div class="row">
    <div class="d-flex">
      <Button
        @btnClick="toggleForm"
        :text="showNoteForm ? 'Close' : 'Add Note'"
        :bgColor="showNoteForm ? 'red' : 'green'"
        :textColor="'white'"
        class="cus-btn ms-auto mb-2"
      />
    </div>
    <NoteForm
      v-show="showNoteForm"
      @add-note="emitAdd"
      @upd-note="emitUpd"
      :showButtonUpd="showButtonUpd"
      :showButtonAdd="showButtonAdd"
    />
    <div :key="note.id" v-for="note in notes">
      <Note
        @selected-note="emitSelectedNote"
        @delete-note="$emit('delete-note', note.id)"
        :note="note"
      />
    </div>
  </div>
</template>

<script>
import Button from "../Button.vue"
import Note from "./note/Note.vue"
import NoteForm from "./note/NoteForm.vue"
export default {
  name: "Notes",
  props: {
    notes: Array,
  },
  data() {
    return {
      showNoteForm: false,
      showButtonUpd: true,
      showButtonAdd: true,
    }
  },
  components: {
    Button,
    Note,
    NoteForm,
  },
  methods: {
    toggleForm() {
      this.showNoteForm = !this.showNoteForm
      this.showButtonUpd = false
      this.showButtonAdd = true
    },
    emitSelectedNote(id) {
      this.showNoteForm = !this.showNoteForm
      this.showButtonUpd = true
      this.showButtonAdd = false
      this.$emit("selected-note", id)
    },
    emitAdd(note) {
      this.$emit("add-note", note)
    },
    emitUpd(note) {
      this.$emit("upd-note", note)
    },
  },
  emits: ["add-note", "delete-note", "selected-note", "upd-note"],
}
</script>

<style></style>
