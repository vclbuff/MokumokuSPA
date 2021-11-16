<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="12" md="12">
      <v-card>
        <v-card-title class="headline">
          自己紹介
        </v-card-title>
        <OrganismsForm
          :base-url="baseUrl"
          :editing-id="editingId"
          :initial-name="editingName"
          :initial-greeting="editingGreeting"
          @posted="getPosts"
          @reset="reset"
        />
        <OrganismsCardList
          :posts="posts"
          @editPost="editPost"
          @deletePost="deletePost"
        />
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
export default {
  data () {
    return {
      baseUrl: 'https://restful.vclbuff.com/api/members',
      posts: [],
      editingId: null
    }
  },
  fetch () {
    this.getPosts()
  },
  computed: {
    editingName () {
      if (this.editingId) {
        const post = this.posts
          .find(item => item.id === this.editingId)
        return post.name
      } else {
        return ''
      }
    },
    editingGreeting () {
      if (this.editingId) {
        const post = this.posts
          .find(item => item.id === this.editingId)
        return post.greeting
      } else {
        return ''
      }
    }
  },
  methods: {
    async getPosts () {
      this.posts = await this.$axios.get(this.baseUrl)
        .then(response => response.data)
    },
    editPost (id) {
      this.editingId = id
    },
    deletePost (id) {
      const result = confirm('投稿内容を削除しますか？')
      if (!result) {
        return
      }
      this.$axios.delete(`${this.baseUrl}/${id}`)
        .then((response) => {
          this.posts = this.posts
            .filter(item => item.id !== id)
        })
    },
    reset () {
      this.editingId = null
    }
  }
}
</script>
