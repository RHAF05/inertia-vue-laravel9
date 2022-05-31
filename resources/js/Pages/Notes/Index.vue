<script setup>
import AppLayout from '@/Layouts/AppLayout.vue';
import Welcome from '@/Jetstream/Welcome.vue';
import { Link } from '@inertiajs/inertia-vue3';
import { useForm } from '@inertiajs/inertia-vue3'

defineProps({
    notes: Array
});

const form = useForm({});

const destroy = (id) => {
    if(confirm('Realmente desea eliminar')){
        form.delete(route('notes.destroy',id));
    }
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
                                <h3 class="text-lg text-gray-900">Listado de Notas</h3>
                                <p class="text-sm text-gray-600">Toma el registro Correcto y ejecuta cualquier función (Ver, editar o eliminar)</p>
                                <Link :href="route('notes.create')" class="bg-blue-500 text-white font-bold py-2 px-4 rounded-md">Crear</Link>
                            </div>
                        </div>
                        <div class="md:col-span-2 mt-5 md:mt-0"> <!-- Decimos que ocupe las dos columnas restantes (col-span-2), margen superior en 5 (mt-5) y que en pantallas medianas pones el margen superior en cero (md:mt-0) -->
                            <div class="shadow bg-white md:rounded-md p-4">
                                <table>
                                    <tr v-for="note in notes" :key="note.id">
                                        <td class="border px-4 py-2">{{ note.excerpt }}</td>
                                        <td class="px-4 py-2">
                                            <Link :href="route('notes.show', note.id)">
                                                Ver
                                            </Link>
                                        </td>
                                        <td class="px-4 py-2">
                                            <Link :href="route('notes.edit', note.id)">
                                                Editar
                                            </Link>
                                        </td>
                                        <td class="px-4 py-2">
                                            <Link @click.prevent="destroy(note.id)">
                                                Eliminar
                                            </Link>
                                        </td>
                                    </tr>
                                </table>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </AppLayout>
</template>
