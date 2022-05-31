<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import Welcome from '@/Jetstream/Welcome.vue';
import { Link } from '@inertiajs/inertia-vue3';
import { useForm } from '@inertiajs/inertia-vue3'

const props=defineProps({note: Object});

const form = useForm({
    excerpt:props.note.excerpt,
    content:props.note.content
});

const submit = () => {
    form.put(route('notes.update',props.note.id), form);
};
</script>

<template>
    <AppLayout title="Dashboard">
        <template #header>
            <h2 class="font-semibold text-xl text-gray-800 leading-tight">
                Módulo de Notas
            </h2>
        </template>

        <div class="py-12">
            <div class="max-w-7xl mx-auto sm:px-6 lg:px-8">
                <div class="bg-white overflow-hidden shadow-xl sm:rounded-lg">
                    <div class="md:grid md:grid-cols-3 md:gap-6"> <!-- el signficiado: tabla para pantallas medianas (md:grid), que tenga 3 columnas (md:grid-cols-3) y que tenga un espacio entre columnas de 6 (md:gap-6) -->
                        <div class="md:col-span-1"> <!-- Creamos la primera columna, usamos el md, para indicar que si es más pequeño que pantallas medianas, la columna ocupe toda la pantalla, pero a partir del tamaño mediano ocupe esta configuración -->
                            <div class="px-4 sm:px0"> <!-- en pantallas pequeñas la dejamos sin espacio (sm:px0) -->
                                <h3 class="text-lg text-gray-900">Editar una nota</h3>
                                <p class="text-sm text-gray-600">Si editas no podrás volver al estado anterior</p>
                            </div>
                        </div>
                        <div class="md:col-span-2 mt-5 md:mt-0"> <!-- Decimos que ocupe las dos columnas restantes (col-span-2), margen superior en 5 (mt-5) y que en pantallas medianas pones el margen superior en cero (md:mt-0) -->
                            <div class="shadow bg-white md:rounded-md p-4">
                                <form @submit.prevent="submit">
                                    <label class="block font-medium text-sm text-gray-700">
                                        Resumen
                                    </label>
                                    <textarea
                                        class="form-input w-full rounded-md shadow-sm"
                                        v-model="form.excerpt"
                                    ></textarea>
                                    <div v-if="form.errors.excerpt">{{ form.errors.excerpt }}</div>
                                    <label class="block font-medium text-sm text-gray-700">
                                        Contenido
                                    </label>
                                    <textarea
                                        class="form-input w-full rounded-md shadow-sm"
                                        v-model="form.content"
                                        rows="8"
                                    ></textarea>
                                    <div v-if="form.errors.content">{{ form.errors.content }}</div>
                                    <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-md">Editar</button>
                                </form>

                                <hr class="my-6">

                                <Link :href="route('notes.index')">
                                    Volver
                                </Link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
