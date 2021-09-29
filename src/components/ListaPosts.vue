<template>
	<v-dialog
		v-model="activo"
		transition="slide-x-reverse-transition"
		scrollable>
		<template v-slot:activator="{on}">
			<v-icon v-on="on">mdi-note-search</v-icon>
		</template>

		<v-card>
			<v-card-title>
				<span class="text-h4">Posts de {{usuario}}</span>

				<v-spacer/>
				<v-btn class="error ma-1" @click="cambiarHabilidad(false)">Deshabilitar</v-btn>
				<v-btn class="success" @click="cambiarHabilidad(true)">Habilitar</v-btn>
			</v-card-title>

			<v-card-text>
				<v-card width="400" class="ma-2 elevation-5 d-inline-block" v-for="post in posts" :key="post.id">
					<v-card-actions>
						<span v-if="post.habilitado" class="success pa-2 rounded-pill">HABILITADO</span>
						<span v-if="!post.habilitado" class="error pa-2 rounded-pill">DESHABILITADO</span>
						<v-spacer/>
						<v-checkbox
								v-model="post.seleccionado"
								color="success"
								></v-checkbox>
					</v-card-actions>
					<v-card-title>
						<span class="text-h5">{{post.title}}</span>
					</v-card-title>
					<v-card-text>
						{{post.body}}
					</v-card-text>
				</v-card>
			</v-card-text>

			<v-card-actions>
				<v-btn class="success" @click="activo = false">Volver</v-btn>
			</v-card-actions>
		</v-card>
	</v-dialog>
</template>

<script>
const axios = require("axios").default;

export default {
	name: "ListaPosts",

	props: {
		id: Number,
		usuario: String
	},

	data: () => ({
		activo: false,
		posts: []
	}),

	methods: {
		conseguirPosts() {
			axios.get("https://jsonplaceholder.typicode.com/posts?userID="+this.id)
				.then(res => {
					this.posts = res.data;
					this.posts.forEach((post) => { 
						post.habilitado = true;
					});
				})
				.catch(err => console.error(err));
		},
		cambiarHabilidad(valor) {
			this.posts.forEach(post => {
				if (post.seleccionado) {
					post.habilitado = valor;
					post.seleccionado = false;
				}
			});
		},
	},

	created() {
		this.conseguirPosts();
	}
}
</script>
