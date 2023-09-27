<template>
    <Titulo texto="Ruta con parámetros" />
    <h2>Parámetro {{ $route.params.id }}</h2>
    <img :src="article.image" width="100" height="100" />
    <h3>{{ article.name }}</h3>
    <p>{{ article.species }}</p>
    <p>{{ article.gender }}</p>
    <p>{{ article.status }}</p>
    <p>{{ article.location.name }}</p>
</template>
<script>
import Titulo from '@/components/Titulo.vue';

export default {
    name: "ArticleView",
    components: {
        Titulo
    },
    data() {
        return {
            article: {}
        }
    },
    methods: {
        async consumeArticle() {
            try {
                const data = await fetch(`https://rickandmortyapi.com/api/character/${this.$route.params.id}`)
                const obj = await data.json()
                console.log(obj)
                this.article = obj
            } catch (error) {
                console.log(error);
            }
        }
    },
    created() {
        this.consumeArticle()
    }
}
</script>