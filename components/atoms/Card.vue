<template>
  <v-card color="#333" class="card">
    <div class="card__button">
      <v-icon
        color="green lighten-3"
        @click="editPost(post.id)"
      >
        mdi-pencil
      </v-icon>
      <v-icon
        color="red"
        @click="deletePost(post.id)"
      >
        mdi-delete
      </v-icon>
    </div>
    <v-card-title>
      {{ post.name }}
    </v-card-title>
    <v-card-text>
      {{ post.greeting }}
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
      default: () => {}
    }
  },
  methods: {
    editPost (id) {
      this.$emit('editPost', id)
    },
    deletePost (id) {
      this.$emit('deletePost', id)
    }
  }
}
</script>

<style>
.card {
  position: relative;
}

.card__button {
  position: absolute;
  top: 0;
  right: 0;
}
</style>
