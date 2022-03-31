<template>
  <v-app dark>
    <v-navigation-drawer
      v-model="drawer"
      :mini-variant="miniVariant"
      :clipped="clipped"
      fixed
      app
      src="https://cdn.vuetifyjs.com/images/backgrounds/bg-2.jpg"
    >
      <v-list>
        <v-list-item
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-item-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-action>
          <v-list-item-content>
            <v-list-item-title v-text="item.title" />
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar
      :clipped-left="clipped"
      fixed
      app
    >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
    </v-app-bar>
    <v-main>
      <v-container>
        <Nuxt />
      </v-container>
    </v-main>
    <v-footer
        :absolute="!fixed"
      app
    >
      <span>&copy; {{ new Date().getFullYear() }} bcmray_crazy</span>
    </v-footer>
  </v-app>
</template>

<script>
export default {
  name: 'DefaultLayout',
  data () {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'mdi-home',
          title: '欢迎翻看Codemao api',
          to: '/'
        },
        {
          icon: 'mdi-account',
          title: '岛3-登录',
          to: '/box3/login'
        },
        {
          icon: 'mdi-account-cog',
          title: '岛3-设置',
          to: '/box3/setting'
        },
      ],
      miniVariant: false,
      right: true,
      rightDrawer: false,
      title: 'Codemao Api'
    }
  },
}
</script>
