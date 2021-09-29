<template>
	<v-container>
		<v-simple-table class="elevation-10" :elevation="15">
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
					<td></td>
				</tr>
			</tbody>
		</v-simple-table>
	</v-container>
</template>

<script>
const axios = require("axios").default;

export default {
	name: "ListaUsuarios",

	data: function() {
		return {
			usuarios: [],
		};
	},

	methods: {
		conseguirUsuarios: function() {
			axios.get("https://jsonplaceholder.typicode.com/users")
				.then(res => this.usuarios = res.data)
				.catch(err => console.error(err));
		},
	},

	created() {
		this.conseguirUsuarios();
	},
};
</script>
