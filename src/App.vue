<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
    </v-app-bar>

    <v-main class="pink lighten-4">
			<ListaUsuarios/>
    </v-main>

		<v-footer padless color="primary" class="lighten-1" dark>
			<v-col class="text-center" cols="12">
				<span class="text-h6">Challenge - Joaquín Laks</span>
			</v-col>
		</v-footer>
  </v-app>
</template>

<script>

import ListaUsuarios from './components/ListaUsuarios';

export default {
  name: 'App',

  components: {
    ListaUsuarios,
  },
};
</script>
