<template>
	<v-container>
		<v-simple-table class="elevation-10">
			<!-- HEADERS -->
			<thead>
				<tr>
					<th>Nombre</th>
					<th>Usuario</th>
					<th>Email</th>
					<th>Teléfono</th>
					<th>Website</th>
					<th>Nombre empresa</th>
					<th>Opciones</th>
				</tr>
			</thead>

			<tbody>
				<tr v-for="usuario in usuarios" :key="usuario.id">
					<td>{{usuario.name}}</td>
					<td>{{usuario.username}}</td>
					<td>{{usuario.email}}</td>
					<td>{{usuario.phone}}</td>
					<td>{{usuario.website}}</td>
					<td>{{usuario.company.name}}</td>
					<td>
						<v-icon icon @click="eliminarUsuario(usuario.id)">mdi-delete</v-icon>
						<EditorDialogo :usuario="usuario"/>
						<ListaPosts :id="usuario.id" :usuario="usuario.name"/>
					</td>
				</tr>
			</tbody>
		</v-simple-table>
	</v-container>
</template>

<script>
import EditorDialogo from "./EditorUsuario";
import ListaPosts from "./ListaPosts.vue";

const axios = require("axios").default;
const usersEnd = "https://jsonplaceholder.typicode.com/users";

export default {
	name: "ListaUsuarios",

	components: {
		EditorDialogo,
		ListaPosts,
	},

	data: function() {
		return {
			usuarios: [],
		};
	},

	methods: {
		conseguirUsuarios: function() {
			axios.get(usersEnd)
				.then(res => this.usuarios = res.data)
				.catch(err => console.error(err));
		},

		eliminarUsuario(id) {
			axios.delete(usersEnd + "/" + id)
				.then(() => console.log("eliminado usuario "+id))
				.catch(err => console.error(err));

			// hago el cambio visible manualmente porque la base de datos no se actualiza de verdad
			this.usuarios.forEach((usuario, i) => {
				console.log(i);
				if (usuario.id === id) {
					this.usuarios.splice(i, 1);
				}
			});
		}
	},

	created() {
		this.conseguirUsuarios();
	},
};
</script>
