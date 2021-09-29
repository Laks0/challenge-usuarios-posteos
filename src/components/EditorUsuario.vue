<template>
	<v-dialog
		max-width="600"
		transition="slide-x-reverse-transition"
		v-model="activo"
		persistent>
		<template v-slot:activator="{on}">
			<v-icon v-on="on">mdi-pencil</v-icon>
		</template>
		<v-form>
			<v-card>
				<v-card-title>
					<span class="text-h4">{{usuario.username}}</span>
				</v-card-title>


				<v-card-text>
					<v-row>
						<!-- COLUMNA IZQUIERDA -->
						<v-col>
							<v-text-field
									v-model="usuarioEditado.name"
									label="Nombre"
									required
									></v-text-field>

							<v-text-field
									v-model="usuarioEditado.email"
									label="Email"
									required
									></v-text-field>

							<v-text-field
									v-model="usuarioEditado.phone"
									label="Teléfono"
									required
									></v-text-field>
						</v-col>
						<!-- COLUNA DERECHA -->
						<v-col>
							<v-text-field
									v-model="usuarioEditado.website"
									label="Website"
									required
									></v-text-field>

							<v-text-field
									v-model="usuarioEditado.company.name"
									label="Empresa"
									required
									></v-text-field>
						</v-col>
					</v-row>
				</v-card-text>

				<v-card-actions>
					<v-spacer></v-spacer>
					<v-btn class = "error" text @click="cancelar">
						Cancelar
					</v-btn>
					<v-btn class="success" text @click="guardar">
						Guardar
					</v-btn>
				</v-card-actions>
			</v-card>
		</v-form>
	</v-dialog>
</template>

<script>
const axios = require("axios").default;

export default {
	name: "EditorDialogo",

	props: {
		usuario: Object,
	},

	data: () => ({
		activo: false,
		usuarioEditado: {},
	}),

	methods: {
		cancelar() {
			this.activo = false;
			this.usuarioEditado = Object.assign({}, this.usuario);
		},
		guardar () {
			// lo copio key por key para no perder la referencia
			let key;
			for (key in this.usuarioEditado) {
				this.usuario[key] = this.usuarioEditado[key];
			}

			// PATCH a la base de datos
			axios.patch("https://jsonplaceholder.typicode.com/users/" + this.usuario.id,
				this.usuarioEditado)
				.then(() => console.log("PATH con éxito"))
				.catch(err => console.error(err));

			this.activo = false;
		},
	},

	created() {
		this.usuarioEditado = Object.assign({}, this.usuario);
	}
}
</script>
