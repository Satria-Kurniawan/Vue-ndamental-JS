<template>
  <div class="card mb-2">
    <div class="card-body d-flex justify-content-between">
      <div class="card-body-wrapper">
        <h4>{{ note.title }}</h4>
        <h5>{{ note.description }}</h5>
      </div>
      <div>
        <i
          @click="$emit('selected-note', note.id)"
          class="fas fa-edit me-3"
        ></i>
        <i @click="$emit('delete-note', note.id)" class="fas fa-times"></i>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Note",
  props: {
    note: Object,
  },
}
</script>

<style>
.fa-times {
  color: red;
  cursor: pointer;
}
.fa-edit {
  color: blue;
  cursor: pointer;
}
i:hover {
  transform: scale(1.5);
  transition: all 0.2s ease-in-out;
  filter: brightness(0.8);
}
</style>
