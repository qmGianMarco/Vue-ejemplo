<script setup>
	import { ref, reactive } from 'vue'; 
	import Presupuesto from './components/Presupuesto.vue';
	import ControlPresupuesto from './components/ControlPresupuesto.vue';
	import Modal from './components/Modal.vue';
	import Gasto from './components/Gasto.vue';
	import { generarId } from './helpers';
	import iconoNuevoGasto from './assets/img/nuevo-gasto.svg'

	 const modal = reactive({
		mostrar: false,
		animar: false
	 })

	const presupuesto = ref(0)
	const disponible = ref(0)

	const gasto = reactive({
		nombre: '',
		cantidad: '',
		categoria: '',
		id: null,
		fecha: Date.now()
	})

	const gastos = ref([])

    const definirPresupuesto = (cantidad) => {
        presupuesto.value = cantidad
		disponible.value = cantidad
    }

	const mostrarModal = () => {
		modal.mostrar = true
		setTimeout(() => {
			modal.animar = true
		}, 300);		
	}

	const ocultarModal = () => {
		modal.animar = false
		setTimeout(() => {
			modal.mostrar = false
		}, 300);
	}

	const guardarGasto = () => {
		gastos.value.push({
			...gasto, /* extrae todos los datos del reactive para que dejen de ser reactivos */
			id: generarId()
		})

		ocultarModal()

		//Reiniciar el objeto
		Object.assign(gasto, {
			nombre: '',
			cantidad: '',
			categoria: '',
			id: null,
			fecha: Date.now()
		})
	}
</script>

<template>
	<div>
		<header>
			<h1>Planificador de gastos</h1>
			<div class="contenedor-header contenedor sombra">
				<Presupuesto
					v-if="presupuesto === 0"
					@definir-presupuesto="definirPresupuesto"
				/>
				<ControlPresupuesto
					v-else
					:presupuesto="presupuesto"
					:disponible="disponible"
				/>
			</div>
		</header>
		<main v-if="presupuesto > 0">

			<div class="listado-gastos contenedor">
				<h2>{{ gastos.length > 0 ? 'Gastos' : 'No hay gastos' }}</h2>

				<Gasto
					v-for="gasto in gastos"
					:key="gasto.id"
					:gasto="gasto"
				/>
			</div>

			<div class="crear-gasto">
				<img
					:src="iconoNuevoGasto"
					alt="icono nuevo gasto"
					@click="mostrarModal"
				> <!-- porque es imagen @click -->
			</div>

			<Modal
				v-if="modal.mostrar"
				@ocultar-modal="ocultarModal"
				@guardar-gasto="guardarGasto"
				:modal="modal"
				v-model:nombre="gasto.nombre"
				v-model:cantidad="gasto.cantidad"
				v-model:categoria="gasto.categoria"
			/> <!-- porque es componente @nombreDeFuncion -->
		</main>
	</div>
</template>

<style>
	:root {
		--azul: #3b82f6;
		--blanco: #fff;
		--gris-claro: #f5f5f5;
		--gris: #94a3e8;
		--gris-oscuro: #64748b;
		--negro: #000;
	}
	html {
		font-size: 62.5%;
		box-sizing: border-box;
	}
	*,
	*:before,
	*:after {
		box-sizing: inherit;
	}
	body {
		font-size: 1.6rem;
		font-family: "Lato", sans-serif;
		background-color: var(--gris-claro);
	}
	h1 {
		font-size: 4rem;
	}
	h2 {
		font-size: 3rem;
	}
	header {
		background-color: var(--azul);
	}
	header h1 {
		padding: 3rem 0;
		margin: 0;
		color: var(--blanco);
		text-align: center;
	}
	.contenedor {
		width: 90%;
		max-width: 80rem;
		margin: 0 auto;
	}
	.contenedor-header {
		margin-top: -5rem;
		transform: translateY(5rem);
		padding: 5rem;
	}
	.sombra {
		box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 1);
		background-color: var(--blanco);
		border-radius: 1.2rem;
		padding: 5rem;
	}
	.crear-gasto {
		position: fixed;
		bottom: 5rem;
		right: 5rem;
	}
	.crear-gasto img {
		width: 5rem;
		cursor: pointer;
	}
	.listado-gastos {
		margin-top: 10rem;
	}
	.listado-gastos h2 {
		font-weight: 900;
		color: var(--gris-oscuro);
	}
</style>
