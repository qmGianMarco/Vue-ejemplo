<script setup>
defineEmits(['actualizar-paciente', 'eliminar-paciente'])

const props = defineProps ({
    paciente: {
        type: Object,
        required: true
    }
})

</script>

<template>
    <div class="px-5 py-10 mx-5 my-10 bg-white shadow-md rounded-xl">
        <p class="mb-3 font-bold text-gray-700 uppercase">ID:
            <span class="font-normal normal-case">
                {{ paciente.id }}
            </span>
        </p>

        <p class="mb-3 font-bold text-gray-700 uppercase">Nombre:
            <span class="font-normal normal-case">
                {{ paciente.nombre }}
            </span>
        </p>

        <p class="mb-3 font-bold text-gray-700 uppercase">Propietario: 
            <span class="font-normal normal-case">
                {{ paciente.propietario }}
            </span>
        </p>

        <p class="mb-3 font-bold text-gray-700 uppercase">Email: 
            <span class="font-normal normal-case">
                {{ paciente.correo }}
            </span>
        </p>

        <p class="mb-3 font-bold text-gray-700 uppercase">Fecha Alta:
            <span class="font-normal normal-case">
                {{ paciente.alta }}
            </span>
        </p>

        <p class="mb-3 font-bold text-gray-700 uppercase">Síntomas:
            <span class="font-normal normal-case">
                {{ paciente.sintomas }}
            </span>
        </p>

        <div class="grid gap-5 mt-10 md:grid-cols-2 ">
            <button 
                type="button"
                class="block w-full px-10 py-2 font-bold text-white uppercase bg-indigo-600 rounded-lg hover:bg-indigo-700"
                @click="$emit('actualizar-paciente', paciente.id)"
            >Editar</button>

            <button 
                type="button"
                class="block w-full px-10 py-2 font-bold text-white uppercase bg-red-600 rounded-lg hover:bg-red-700"
                @click="$emit('eliminar-paciente', paciente.id)"
            >Eliminar</button>
        </div>
    </div>
</template>

