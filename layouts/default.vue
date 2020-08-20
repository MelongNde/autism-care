<template>
  <v-app>
    <v-navigation-drawer v-model="drawer" :right="right" :mini-variant="miniVariant" :src="bg" light dark app>
      <v-list-item two-line :class="miniVariant && 'px-0'">
        <v-list-item-avatar>
          <img src="https://scontent.fdla1-1.fna.fbcdn.net/v/t1.0-9/90218853_2595603497386136_6086761805747585024_o.jpg?_nc_cat=100&_nc_sid=09cbfe&_nc_ohc=swlemybvek8AX96Htct&_nc_ht=scontent.fdla1-1.fna&oh=86b1517fbb9273909facfe71234d07a4&oe=5F4DB65C">
        </v-list-item-avatar>
        <v-list-item-content>
          <v-list-item-title>Brice Nde</v-list-item-title>
          <v-list-item-subtitle>Online</v-list-item-subtitle>
        </v-list-item-content>
      </v-list-item>

      <v-divider />
      <v-list>
        <v-list-item v-for="(item, i) in items" :key="i" :to="item.to" router>
          <v-list-item-action>
            <v-icon v-html="item.icon" />
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar :clipped-left="clipped" class="blue" fixed app>
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />

      <v-toolbar-title>My files</v-toolbar-title>

      <v-spacer />

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-filter</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>
    <!-- <v-app-bar :clipped-left="clipped" class="blue" fixed app>
      <v-app-bar-nav-icon @click="drawer = !drawer" />
      <v-toolbar-title v-html="title" />
      <v-btn icon>
        <v-icon>mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar> -->
    <v-main class="background-color: blue lighten-5 content" style="color: #222831" light>
      <v-container fluid>
        <nuxt light />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
/* eslint-disable */
export default {
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        { icon: 'home', title: 'Welcome', to: '/' },
        { icon: 'school', title: 'Learn', to: '/learn' },
        { icon: 'people', title: 'Users', to: '/users' },
        { icon: 'wallpaper', title: 'Train', to: '/train' },
        { icon: 'camera', title: 'Recognize', to: '/recognize' },
        { icon: 'reduce_capacity', title: 'Find the pairs', to: '/findThePairs' },
        { icon: 'history_edu', title: 'Quiz', to: '/quiz' }
      ],
      right: false,
      rightDrawer: false,
      title: 'AutismCare',
      color: 'primary',
      colors: [
        'primary',
        'blue',
        'success',
        'red',
        'teal'
      ],
      permanent: true,
      miniVariant: false,
      expandOnHover: false,
      background: true
    }
  },
  computed: {
    loading () {
      return this.$store.state.face.loading
    },
    bg () {
      return this.background ? 'https://cdn.vuetifyjs.com/images/backgrounds/bg-2.jpg' : undefined
    }
  },
  created () {
    this.$vuetify.theme.dark = true
  },
  async mounted () {
    const self = this
    await self.$store.dispatch('face/load')
  }
}
</script>
 <style>
  *{
    font-family: Helvetica-light, sans-serif;
  }
 </style>
