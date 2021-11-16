<template>
  <v-form
    ref="form"
    v-model="valid"
  >
    <v-container>
      <v-row justify="center">
        <v-col cols="12" sm="8" md="10">
          <v-text-field
            v-model="name"
            :counter="20"
            :rules="nameRules"
            label="お名前"
            required
          />
        </v-col>
        <v-col cols="12" sm="8" md="10">
          <v-textarea
            v-model="greeting"
            outlined
            label="自己紹介文"
            :counter="255"
            :rules="greetingRules"
          />
        </v-col>
      </v-row>
      <v-row justify="end" aling="center">
        <v-col cols="12" sm="2" md="2">
          <v-btn
            v-if="!id"
            color="primary"
            elevation="2"
            class="submit"
            @click="post"
          >
            {{ submitButton }}
          </v-btn>
          <v-btn
            v-else
            color="primary"
            elevation="2"
            class="submit"
            @click="editPost"
          >
            {{ submitButton }}
          </v-btn>
          <v-btn
            v-if="id"
            color="red"
            elevation="2"
            class="submit"
            @click="reset"
          >
            リセット
          </v-btn>
        </v-col>
      </v-row>
    </v-container>
  </v-form>
</template>

<script>
export default {
  props: {
    baseUrl: {
      type: String,
      required: true,
      default: ''
    },
    editingId: {
      type: Number,
      required: false,
      default: null
    },
    initialName: {
      type: String,
      required: false,
      default: ''
    },
    initialGreeting: {
      type: String,
      required: false,
      default: ''
    }
  },
  data () {
    return {
      valid: true,
      name: '',
      nameRules: [
        v => !!v || 'お名前を入力してください。',
        v => (v && v.length <= 20) || '20文字以内で入力してください。'
      ],
      greeting: '',
      greetingRules: [
        v => !!v || '自己紹介を入力してください。',
        v => (v && v.length <= 255) || '255文字以内で入力してください。'
      ]
    }
  },
  computed: {
    id () {
      return this.editingId
    },
    submitButton () {
      return this.editingId ? '更新する' : '送信する'
    }
  },
  watch: {
    initialName (value) {
      this.name = value
    },
    initialGreeting (value) {
      this.greeting = value
    }
  },
  methods: {
    post () {
      if (!this.$refs.form.validate()) {
        return
      }
      const params = {
        name: this.name,
        greeting: this.greeting
      }

      this.$axios.post(this.baseUrl, params)
        .then(() => {
          this.greeting = ''
          this.$refs.form.resetValidation()
          this.$emit('posted')
        })
    },
    editPost () {
      const params = {
        name: this.name,
        greeting: this.greeting
      }

      this.$axios.patch(`${this.baseUrl}/${this.editingId}`, params)
        .then(() => {
          this.greeting = ''
          this.$refs.form.resetValidation()
          this.$emit('posted')
        })
    },
    reset () {
      this.$emit('reset')
      this.$refs.form.resetValidation()
    }
  }
}
</script>

<style>
.submit {
  margin-bottom: 16px;
}
</style>
