<template>
  <div>
    <v-row align="center">
      <v-col
        v-for="post in posts"
        :key="post.id"
        cols="12"
        sm="4"
        md="4"
      >
        <AtomsCard
          :post="post"
          @editPost="editPost"
          @deletePost="deletePost"
        />
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  props: {
    posts: {
      type: Array,
      required: true,
      default: () => []
    }
  },
  methods: {
    deletePost (id) {
      this.$emit('deletePost', id)
    },
    editPost (id) {
      this.$emit('editPost', id)
    }
  }
}
</script>
