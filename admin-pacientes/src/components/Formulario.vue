<script setup>
    import { reactive, computed } from 'vue';
    import Alerta from './Alerta .vue';

    const alerta = reactive({
        tipo:'',
        mensaje:''
    })

    const emit = defineEmits(['update:nombre', 'update:propietario', 'update:correo', 'update:alta', 'update:sintomas',
     'guardar-paciente'])

    const props = defineProps({
        id: {
            type: [String, null],
            required: true
        },
        nombre: {
            type: String,
            required: true
        },
        propietario: {
            type: String,
            required: true
        },
        correo: {
            type: String,
            required: true
        },
        alta: {
            type: String,
            required: true
        },
        sintomas: {
            type: String,
            required: true
        }
    })

    const validar = () => {
        if (Object.values(props).includes('')){
            alerta.mensaje = 'Todos los campos son obligatorios';
            alerta.tipo = 'error'
            return
        }

        emit('guardar-paciente')
        alerta.mensaje = 'Paciente agregado correctamente'
        alerta.tipo = 'exito'

        setTimeout(() => {
            Object.assign(alerta, {
                tipo:'',
                mensaje:''
            })
        }, 3000)
    }

    const editando = computed(() => {
        return props.id
    })

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="text-3xl font-black text-center">Seguimiento pacientes</h2>

        <p class="mt-5 mb-10 text-lg text-center">
            Añade Pacientes y
            <span class="font-bold text-indigo-600">Administralos</span>
        </p>

        <Alerta
            v-if="alerta.mensaje"
            :alerta="alerta"
        />
        <form
            class="px-5 py-10 mb-10 bg-white rounded-lg shadow-md"
            @submit.prevent="validar"
        >
            <div class="mb-5">
                <label
                    for="mascota"
                    class="block font-bold text-gray-700 uppercase"
                >
                    Nombre mascota
                </label>
                <input
                    id="mascota"
                    type="text"
                    placeholder="Nombre de la mascota"
                    class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
                    :value="nombre"
                    @input="$emit('update:nombre', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label
                    for="propietario"
                    class="block font-bold text-gray-700 uppercase"
                >
                    Nombre propietario
                </label>
                <input
                    id="propietario"
                    type="text"
                    placeholder="Nombre del propietario"
                    class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
                    :value="propietario"
                    @input="$emit('update:propietario', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label
                    for="email"
                    class="block font-bold text-gray-700 uppercase"
                >
                    Correo
                </label>
                <input
                    id="email"
                    type="email"
                    placeholder="Correo del propietario"
                    class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
                    :value="correo"
                    @input="$emit('update:correo', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label
                    for="alta"
                    class="block font-bold text-gray-700 uppercase"
                >
                    Alta
                </label>
                <input
                    id="alta"
                    type="date"
                    placeholder="Fecha de alta"
                    class="w-full p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
                    :value="alta"
                    @input="$emit('update:alta', $event.target.value)"
                />
            </div>

            <div class="mb-5">
                <label
                    for="sintomas"
                    class="block font-bold text-gray-700 uppercase"
                >
                    Sintomas
                </label>
                <textarea
                    id="sintomas"
                    type="text"
                    placeholder="Describe los síntomas"
                    class="w-full h-40 p-2 mt-2 placeholder-gray-400 border-2 rounded-md"
                    :value="sintomas"
                    @input="$emit('update:sintomas', $event.target.value)"
                />
            </div>

            <input
                type="submit"
                class="w-full p-3 font-bold text-white uppercase transition-colors bg-indigo-600 cursor-pointer hover:bg-indigo-700"
                :value="[editando ? 'Guardar cambios' : 'Registrar paciente']"
            />
        </form>
    </div>
</template>