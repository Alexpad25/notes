<template>
  <div class="new-note">
    <label for="">Title</label>
    <input v-model="note.title" type="text">
    <label for="">Description</label>
    <textarea v-model="note.descr" name="" id="" cols="30" rows="10"></textarea>
    <button class="btn btnPrimary" @click="addNote">New note</button>
  </div>
</template>

<script>
export default {
  props: {
    note: {
      type: Object,
      required: true
    }
  },
  methods: {
    addNote() {
      return this.$emit('addNote', this.note);
    }
  }
}
</script>

<style lang="scss" scoped>
  .new-note {
    text-align: center;
  }
  button {
    margin: 20px;
  }
</style>