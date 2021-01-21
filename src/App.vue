<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      :mobile-breakpoint="768"
      app
    >

    <!-- opção de bg lateral -->
      <v-img
        class="pa-4 pt-7"
        src="notes.jpg"
        height="170"
        gradient="to top right, rgba(98,0,234,1), rgba(98,0,234,1)"
      >

        <v-avatar size="70" class="mb-2">
          <img
            src="https://s.gravatar.com/avatar/5258e24f357f8bb0adeb242a63181f4e?s=80"
            alt="Andersondcribeiro"
          >
        </v-avatar>
        <div class="white--text text-subtitle-1 font-weight-bold">
          Anderson Ribeiro
        </div>
        <!--div class="white--text text-subtitle-2">
          anderson_ribeiro
        </!--div-->
      </v-img>

      <v-list
        dense
        nav
      >
      <!-- propriedade da lista do menu -->
        <v-list-item
          v-for="item in items"
          :key="item.title"
          :to="item.to"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>
    </v-navigation-drawer>

    <v-app-bar
      app
      color="deep-purple accent-4"
      dense
      dark 
      prominent
      :height="$route.path === '/' ? '238' : '170'"
 
    >
    <!-- opção de usar cor de fundo navigation drawer com imagem ou gradiente!-->
      <!--template v-slot:img="{ props }">
        <v-img
          v-bind="props"
          gradient="to top right, rgba(156, 165, 29,1), rgba(12,13,2,1)"
        ></v-img>
      </!--template-->

      <v-container class="header-container pa-0">
        <v-row>
          <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>
          <v-spacer></v-spacer>
          <search />
        </v-row>
        <v-row>

          <!-- titulo do app -->
          <v-toolbar-title class="text-h4 ml-4">
            {{ $store.state.appTitle }}
          </v-toolbar-title>
        </v-row>

        <!-- data e hora -->
        <v-row>
          <live-date-time />
        </v-row >
        <v-row v-if="$route.path === '/'">
          <field-add-task />
        </v-row>
      </v-container>

    </v-app-bar>

    <v-main>
      <router-view></router-view>
      <snackbar />
    </v-main>
  </v-app>
</template>


<!-- menu lateral - navigation drawer  --> 
<script>
  export default {
    data: () => ({
      drawer: null,
      items: [
        { title: 'Lista de Tarefas', icon: 'mdi-format-list-checks', to: '/' },
        { title: 'Sobre', icon: 'mdi-help-box', to: '/sobre' },
        /*{ title: 'FAQ', icon: 'mdi-frequently-asked-questions', to: '/faq'},*/
        /*{ title: 'Usuário', icon:'mdi-account-circle-outline', to: '/usuario'}*/
      ],
    }),
    mounted() {
      this.$store.dispatch('getTasks')
    },
    components: {
      'search': require('@/components/Tools/Search.vue').default,
      /*'live-date-time': require('@/components/Tools/LiveDateTime.vue').default,*/
      'field-add-task': require('@/components/Todo/FieldAddTask.vue').default,
      'snackbar': require('@/components/Shared/Snackbar.vue').default
    }
  }
</script>

<style lang="sass">
  .header-container
    max-width: none
</style>