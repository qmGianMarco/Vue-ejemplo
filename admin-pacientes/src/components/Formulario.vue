<script setup>
    import { reactive } from 'vue';

    const paciente = reactive({
        nombre: '',
        propietario: '',
        correo: '',
        alta: '',
        sintomas: ''
    })

</script>

<template>
    <div class="md:w-1/2">
        <h2 class="text-3xl font-black text-center">Seguimiento pacientes</h2>

        <p class="mt-5 mb-10 text-lg text-center">
            Añade Pacientes y
            <span class="font-bold text-indigo-600">Administralos</span>
        </p>

        <form
            class="px-5 py-10 mb-10 bg-white rounded-lg shadow-md"
        >
        {{ paciente.nombre }}
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
                    v-model="paciente.nombre"
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
                />
            </div>

            <input
                type="submit"
                class="w-full p-3 font-bold text-white uppercase transition-colors bg-indigo-600 cursor-pointer hover:bg-indigo-700"
                value="Registrar Paciente"
            />
        </form>
    </div>
</template>