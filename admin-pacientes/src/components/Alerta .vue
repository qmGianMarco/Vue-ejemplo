<script setup>
    import { computed } from 'vue';

    const props = defineProps({
        alerta: {
            type: Object,
            required: true
        }
    })

    const isError = computed(() => {
        return props.alerta.tipo === 'error'
    })
</script>

<template>
    <div
        :class="[isError ? 'bg-red-500' : 'bg-green-500']"
        class="p-3 mb-3 font-bold text-center text-white rounded-md"
    >
        {{ alerta.mensaje }}
    </div>
</template>

