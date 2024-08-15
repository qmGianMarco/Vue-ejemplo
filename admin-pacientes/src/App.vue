<script setup>
	import { ref, reactive } from 'vue';
	import Header from './components/Header.vue';
	import Formulario from './components/Formulario.vue';
	import Paciente from './components/Paciente.vue';

	const pacientes = ref([])

	const paciente = reactive({
        nombre: '',
        propietario: '',
        correo: '',
        alta: '',
        sintomas: ''
    })

const guardarPaciente = () => {
	pacientes.value.push(paciente)
	
}

</script>

<template>
	<div class="container mx-auto mt-20">
		<Header />

		<div class="mt-12 md:flex">
			<Formulario 
				v-model:nombre="paciente.nombre"
				v-model:propietario="paciente.propietario"
				v-model:correo="paciente.correo"
				v-model:alta="paciente.alta"
				v-model:sintomas="paciente.sintomas"
				@guardar-paciente="guardarPaciente"
			/>

			<div class="overflow-y-scroll md:w-1/2 md:h-screen">
				<h3 class="text-3xl font-black text-center">Administra tus pacientes</h3>

				<div v-if="pacientes.length > 0">
					<p class="mt-5 mb-10 text-lg text-center">
						Información de
						<span class="font-bold text-indigo-600">Pacientes</span>
					</p>

					<Paciente
						v-for="paciente in pacientes"
						:paciente="paciente"
					/>
				</div>
				<p v-else class="mt-20 text-2xl text-center" >No hay pacientes</p>
			</div>
		</div>
	</div>
</template>

