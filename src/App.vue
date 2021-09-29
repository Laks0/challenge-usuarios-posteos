<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
			<span class="text-h4 hidden-sm-and-down"><b>ADMIN DE USUARIOS</b></span>
			<v-spacer></v-spacer>

			<v-btn outlined 
				href="https://github.com/Laks0/challenge-usuarios-posteos/"
				target="_blank">
				Proyecto en github</v-btn>
    </v-app-bar>

    <v-main class="pink lighten-4">
			<ListaUsuarios/>
    </v-main>

		<v-footer padless color="primary" dark>
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
