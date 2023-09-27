<template>
    <Titulo texto="Página de Blog" />
    <!-- <button @click="consumirAPI">Consumir API</button> -->
    <div>
        <table>
            <thead>
                <tr>
                    <th>#</th>
                    <th>Image</th>
                    <th>Nombre</th>
                    <th>Especie</th>
                    <th>Género</th>
                    <th>Estado</th>
                </tr>
            </thead>
            <tbody v-for="item in arrayBlog" :key="item.id">
                <tr>
                    <td>{{ item.id }}</td>
                    <router-link :to="`/blog/${item.id}`">
                        <td><img :src="item.image" width="100" height="100" /></td>
                    </router-link>

                    <td>{{ item.name }}</td>
                    <td>{{ item.species }}</td>
                    <td>{{ item.gender }}</td>
                    <td>{{ item.status }}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>
<script>
import Titulo from '@/components/Titulo.vue';
export default {
    name: "BlogView",
    components: {
        Titulo
    },
    data() {
        return {
            arrayBlog: []
        }
    },
    methods: {
        async consumeAPI() {
            try {
                const data = await fetch('https://rickandmortyapi.com/api/character');
                const array = await data.json()
                console.log(array);
                this.arrayBlog = array.results
            } catch (error) {
                console.log(error);
            }
        }
    },
    created() {
        this.consumeAPI()
    }
}
</script>