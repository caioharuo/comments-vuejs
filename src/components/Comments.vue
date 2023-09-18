<template>
  <div class="container">
    <h1>Comentários</h1>
    <hr />

    <FormTodo v-on:add-comment="addComment" />

    <div class="list-group">
      <p v-if="comments.length <= 0">Sem comentários...</p>

      <div
        class="list-group-item"
        v-for="(comment, index) in allComments"
        v-bind:key="index"
      >
        <span class="comment_author"
          >Autor: <strong>{{ comment.name }}</strong></span
        >
        <p>{{ comment.message }}</p>
        <div>
          <a
            href="#"
            title="Excluir"
            v-on:click.prevent="handleRemoveComment(index)"
            >Excluir</a
          >
        </div>
      </div>
    </div>
    <hr />
  </div>
</template>

<script lang="ts">
import FormTodo from './FormComments.vue';

export default {
  components: {
    FormTodo,
  },
  data() {
    return {
      comments: [] as Array<{ name: string; message: string }>,
    };
  },
  methods: {
    addComment(comment: { name: string; message: string }) {
      this.comments.push({ name: comment.name, message: comment.message });
    },
    handleRemoveComment(index: number) {
      this.comments.splice(index, 1);
    },
  },
  computed: {
    allComments() {
      return this.comments.map(
        (comment: { name: string; message: string }) => ({
          ...comment,
          name: comment.name.trim() === '' ? 'Anônimo' : comment.name,
        })
      );
    },
  },
};
</script>
