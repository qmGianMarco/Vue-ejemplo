<script setup>
	import { ref, reactive, onMounted, watch } from 'vue';
	import { uid } from 'uid';
	import Header from './components/Header.vue';
	import Formulario from './components/Formulario.vue';
	import Paciente from './components/Paciente.vue';

	const pacientes = ref([])

	watch(pacientes, () => {
		guardarLocalStorage()
	}, {
		deep: true
	})

	onMounted(() => {
		const pacientesStorage = localStorage.getItem('pacientes')
        if (pacientesStorage) {
            pacientes.value = JSON.parse(pacientesStorage)
        }
	})

	const guardarLocalStorage = () => {
        localStorage.setItem('pacientes', JSON.stringify(pacientes.value))
    }

	const paciente = reactive({
		id: null,
        nombre: '',
        propietario: '',
        correo: '',
        alta: '',
        sintomas: ''
    })

	const guardarPaciente = () => {
		if (paciente.id) {
			const { id } = paciente
			const i = pacientes.value.findIndex(paciente => paciente.id === id )
			pacientes.value[i] = {...paciente}		
		} else {
			pacientes.value.push({
				...paciente, //enviar una copia no reactiva del objeto
				id: uid()
			})
		}

		//Reiniciar paciente
		Object.assign(paciente, {
			nombre: '',
			propietario: '',
			correo: '',
			alta: '',
			sintomas: '',
			id: null
		})
	}

	const actualizarPaciente = (id) => {
		const pacienteEditar = pacientes.value.filter( paciente => paciente.id === id )[0]
		Object.assign(paciente, pacienteEditar)		
	}

	const eliminarPaciente = (id) => {
		pacientes.value = pacientes.value.filter(paciente => paciente.id !== id)
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
				:id="paciente.id"
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
						@actualizar-paciente="actualizarPaciente"
						@eliminar-paciente="eliminarPaciente"
					/>
				</div>
				<p v-else class="mt-20 text-2xl text-center" >No hay pacientes</p>
			</div>
		</div>
	</div>
</template>

