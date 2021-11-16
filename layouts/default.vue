<template>
  <v-app dark>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <h1 class="heading">
        もくもくしよう木曜日 RESTful API入門
      </h1>
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
      :absolute="!fixed"
      app
      class="footer"
    >
      <v-row justify="space-around" align="center">
        <span>&copy; {{ new Date().getFullYear() }} vclbuff</span>
        <a
          href="https://discord.gg/wVCPhuDUen"
          target="_blank"
          rel="noopener noreferrer"
          class="join"
        >
          <v-btn
            color="secondary lighten-1"
            elevation="2"
          >
            Join Discord
          </v-btn>
        </a>
      </v-row>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-apps',
          title: 'Welcome',
          to: '/'
        },
        {
          icon: 'mdi-chart-bubble',
          title: 'Inspire',
          to: '/inspire'
        }
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Vuetify.js'
    }
  }
}
</script>

<style>
.heading {
  font-size: 1.2rem;
}

@media all and (min-width: 500px) {
  .heading {
    font-size: 1.5rem;
  }
}

.footer {
  height: 60px;
}

.join {
  text-decoration: none;
}
</style>
