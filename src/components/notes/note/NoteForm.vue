<template>
  <form class="mb-4">
    <div class="mb-3">
      <label for="title" class="form-label">Title</label>
      <input
        type="text"
        class="form-control"
        v-model="title"
        name="title"
        placeholder="Input title..."
      />
    </div>
    <div class="mb-3">
      <label for="description" class="form-label">Description</label>
      <input
        type="text"
        class="form-control"
        v-model="description"
        name="description"
        placeholder="Input description..."
      />
    </div>
    <Button
      v-show="showButtonAdd"
      @click="handleAdd"
      :text="'Add'"
      :bgColor="'black'"
      :textColor="'white'"
      class="cus-btn me-2"
    />
    <Button
      v-show="showButtonUpd"
      @click="handleUpdate"
      :text="'Update'"
      :bgColor="'blue'"
      :textColor="'white'"
      class="cus-btn"
    />
  </form>
</template>

<script>
import Button from "../../../components/Button.vue"

export default {
  name: "NoteForm",
  components: {
    Button,
  },
  props: {
    showButtonUpd: Boolean,
    showButtonAdd: Boolean,
  },
  data() {
    return {
      title: "",
      description: "",
    }
  },
  methods: {
    hideShowButton() {
      this.showButton = !this.showButton
    },
    handleAdd(e) {
      e.preventDefault()

      const newNotes = {
        title: this.title,
        description: this.description,
      }

      this.$emit("add-note", newNotes)

      this.title = ""
      this.description = ""
    },
    handleUpdate(e) {
      e.preventDefault()

      const newNotes = {
        title: this.title,
        description: this.description,
      }

      this.$emit("upd-note", newNotes)

      this.title = ""
      this.description = ""
    },
  },
}
</script>
