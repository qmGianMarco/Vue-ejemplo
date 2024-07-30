<script setup>
	import { ref, onMounted } from 'vue'
	import { db } from './data/guitarras'
	import Guitarra from './components/Guitarra.vue'
    import Header from "./components/Header.vue";
    import Footer from './components/Footer.vue';

	/* Para arrays, bool, strings, etc */
	const guitarras = ref([])
    const carrito = ref([])
    const guitarra = ref({})

	/* Metodo del ciclo de vida */
	/* Ejecuta lo que tiene cuando el componente esta listo */
	onMounted(() => {
		guitarras.value = db;
        guitarra.value = db[3]
	})

	const agregarCarrito = (guitarra) => {
        const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)

        if (existeCarrito >= 0){
            carrito.value[existeCarrito].cantidad++
        }else{
            guitarra.cantidad = 1;
            carrito.value.push(guitarra);
        }
    }

    const decrementarCantidad = (id) => {
        const index = carrito.value.findIndex(producto => producto.id === id)
        if (carrito.value[index].cantidad <= 1) return
        carrito.value[index].cantidad--
    }

    const incrementarCantidad = (id) => {
        const index = carrito.value.findIndex(producto => producto.id === id)
        if (carrito.value[index].cantidad >= 5) return
        carrito.value[index].cantidad++
    }

    const eliminarProducto = (id) => {
        carrito.value = carrito.value.filter(producto => producto.id != id)
    }

    const vaciarCarrito = () => {
        carrito.value = []
    }

</script>

<template>
	<Header 
    :carrito="carrito"
    :guitarra="guitarra"
    @incrementar-cantidad="incrementarCantidad"
    @decrementar-cantidad="decrementarCantidad"
    @agregar-carrito="agregarCarrito"
    @eliminar-producto="eliminarProducto"
    @vaciar-carrito="vaciarCarrito"
    ></Header>

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
			<Guitarra 
				v-for="guitarra in guitarras"
				v-bind:guitarra="guitarra"
				@agregar-carrito="agregarCarrito"
			/> <!-- se envia props y eventos -->
        </div>
    </main>

    <Footer></Footer>
</template>