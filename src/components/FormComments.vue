<template>
  <div class="form-comments form-group">
    <p>
      <input
        placeholder="Nome"
        type="text"
        name="author"
        class="form-control"
        v-model="name"
      />
    </p>
    <p>
      <textarea
        placeholder="Comentário"
        name="message"
        class="form-control"
        v-model="message"
      ></textarea>
    </p>

    <button
      v-on:click="handleComment"
      type="submit"
      class="btn btn-primary mb-3"
    >
      Comentar
    </button>
  </div>
</template>

<script lang="ts" type="module">
export default {
  data() {
    return {
      name: '',
      message: '',
    };
  },
  methods: {
    handleComment() {
      if (this.message.trim() === '') {
        return;
      }

      this.$emit('add-comment', {
        name: this.name,
        message: this.message,
      });

      this.name = '';
      this.message = '';
    },
  },
};
</script>
