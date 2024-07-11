<template>
  <v-app>
    <v-navigation-drawer class=" elevation-2" v-model="isDrawerOpen">
      <v-list>
        <v-list-subheader>Menu</v-list-subheader>
        <v-divider></v-divider>
        <v-list-item prepend-icon="mdi-home">Home</v-list-item>
        <v-list-item prepend-icon="mdi-account">Usuários</v-list-item>
        <v-list-group value="Clientes">
          <template #activator="{ props }">
            <v-list-item v-bind="props" prepend-icon="mdi-account-circle">Clientes</v-list-item>
          </template>
          <v-list-item prepend-icon="mdi-currency-usd">Vendas</v-list-item>
          <v-list-item prepend-icon="mdi-chart-line">Relatórios</v-list-item>
        </v-list-group>
      </v-list>
    </v-navigation-drawer>
    <v-app-bar flat class=" border-b elevation-1">
      <v-app-bar-nav-icon @click="handleShowDrawer"></v-app-bar-nav-icon>
      <v-app-bar-title>
        App
      </v-app-bar-title>
      <template #append>
        <v-menu>
          <template #activator="{props}">
            <v-btn v-bind="props" icon class="mr-2">
              <v-badge color="info" dot>
                <v-icon icon="mdi-bell-outline"></v-icon>
              </v-badge>
            </v-btn>
          </template>
          <v-list class="border-b" nav density="compact" min-width="200px" elevation-2 >
            <v-list-item>
              <v-list-item-subtitle>VIEW READ ({{ howMuchRead }})</v-list-item-subtitle>
            </v-list-item>
          </v-list>
          <v-list class="border-b" nav density="compact" elevation-2 >
            <v-list-item v-for="(notification, i) in notificationItems" :key="i" :value="notification.title">
              <template #prepend>
                <v-icon :icon="notification.firstIcon"></v-icon>
              </template>

              <v-list-item-title> {{ notification.title }} </v-list-item-title>
              <v-list-item-subtitle> {{ notification.description }} </v-list-item-subtitle>

              <template #append>
                <v-icon :icon="notification.lastIcon"></v-icon>
              </template>
            </v-list-item>
          </v-list>
        </v-menu>
        <v-menu>
          <template #activator="{ props }">
            <v-avatar v-bind="props">
              <v-img cover
                src="https://thumbs.dreamstime.com/z/nerd-portrait-young-cheerful-businessman-smiling-36201399.jpg"></v-img>
            </v-avatar>
          </template>
          <v-list nav density="compact" min-width="200px" elevation-2 >
            <v-list-item v-for="(item, i) in profileItems" :key="i" :value="item.text" to="/" :prepend-icon="item.icon">
              <v-list-item-title> {{ item.text }}</v-list-item-title>
            </v-list-item>
          </v-list>
        </v-menu>
      </template>
    </v-app-bar>
    <v-main>
      <v-container>
        <h1>Dashboard</h1>
        <v-row>
          <v-col v-for="(beach, i) in beachCard" :key="i" :value="beach.city" cols="12" sm="6" md="4" lg="3">
            <v-card flat class="border"  >
              <v-img
                cover
                height="250px"
                class=" text-white align-end"
                :src="beach.link"
              >
                <v-card-title class=" text-h6 ">{{ beach.text }}</v-card-title>
              </v-img>
              <v-card-subtitle class=" pt-2 ">{{ beach.city }}</v-card-subtitle>
              <v-card-text>
                <div>{{ beach.description }}</div>
              </v-card-text>
              <v-card-actions>
                <v-btn variant="outlined" color="primary">Ver mais</v-btn>
                <v-btn prepend-icon="mdi-cart" variant="tonal" color="blue">Comprar</v-btn>
              </v-card-actions>
            </v-card>
          </v-col>
        </v-row>
      </v-container>
    </v-main>

  </v-app>
</template>

<script>
export default {
  data() {
    return {
      isDrawerOpen: false,
      howMuchRead: 0,

      profileItems: [
        { text: 'Meu perfil', icon:'mdi-account'},
        { text: 'Favoritos', icon:'mdi-heart'},
      ],

      notificationItems: [
        { firstIcon: 'mdi-heart', lastIcon:'mdi-email-open', description: 'descrição da notificação', title: 'titulo da notificação'},
        { firstIcon: 'mdi-account', lastIcon:'mdi-email-open', description: 'descrição da notificação', title: 'titulo da notificação'},
        { firstIcon: 'mdi-cart', lastIcon:'mdi-email-open', description: 'descrição da notificação', title: 'titulo da notificação'},
      ],

      beachCard: [
        {
          text: 'Praia de Copacabana',
          link: 'https://upload.wikimedia.org/wikipedia/commons/thumb/e/e6/Aerial_view_of_Copacabana_beach.jpg/1200px-Aerial_view_of_Copacabana_beach.jpg',
          city: 'Rio de Janeiro',
          description: 'Praia icônica com calçadão famoso.'
        },
        {
          text: 'Praia do Forte',
          link: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTEGU6Dv8DrMrONaINSHs93rc_8rvxLxQS7ag&s',
          city: 'Cabo Frio',
          description: 'Águas claras e areia branca.'
        },
        {
          text: 'Praia da Pipa',
          link: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRQHbwq0iFcwi8H-dN9WeoTHqpZ_rmpsNHsEw&s',
          city: 'Tibau do Sul',
          description: 'Paraíso com falésias coloridas.'
        },
        {
          text: 'Praia do Sancho',
          link: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcTndRqFqB95CbyahQDfkanB1l6t87PzpHdUog&s',
          city: 'Fernando de Noronha',
          description: 'Considerada uma das praias mais bonitas do mundo.'
        }
      ],


    }
  },
  methods: {
    handleShowDrawer() {
      this.isDrawerOpen = !this.isDrawerOpen
    }
  }
}
</script>
