<template>
    <h1>Ejemplo de Vue.js</h1>
    <h2>Curso administración y programación de sitios web</h2>
    <h2>Colegio Universitario de Cartago</h2>
    <hr/>

    <h3>¿Deseas buscar una receta?</h3>
    <input 
        class="search-input" 
        type="text" 
        v-model="search" 
        v-on:keyup.enter="searchData" 
        placeholder="Buscar receta"
    >
    
    <Meal
        v-for="meal in meals" 
        v-bind:key="meal.idMeal" 
        v-bind:meal="meal"
    />

    <div class="textcenter">
        ...
    </div>

    <h3>O busca por categoría</h3>

    <Category
        v-for="category in paginated" 
        v-bind:key="category.idCategory" 
        v-bind:category="category"
    />

    <div class="textcenter">
        Actual: {{ current }};
    </div>

    <div class="textcenter">
        <a @click="prev()">Anterior</a>
        |
        <a @click="next()">Siguiente</a>
    </div>
</template>

<script>
import Category from './Category.vue';
import Meal from './Meal.vue';
import axios from 'axios';
import Swal from 'sweetalert';

export default {
    name: 'App',
    components: {
    Category,
    Meal,
    },
    data(){
        return {
        categories: [],
        meals: [],
        search: null,
        //Paginación
        current: 1,
        pageSize: 5,
        };
    },
    mounted(){
        axios.get('https://themealdb.com/api/json/v1/1/categories.php')
        .then((res) => {
            this.categories = res.data.categories;
        })
        .catch((err) => {
            console.log(err);
        });
    },
    computed: {
        indexStart(){
            return(this.current - 1) * this.pageSize;
        },
        indexEnd(){
            return this,this.indexStart + this.pageSize;
        },
        paginated(){
            return this.categories.slice(this.indexStart, this.indexEnd);
        },
    },
    methods: {
        searchData(){
            //Verificar si el campo tiene texto
            if(this.search){
                axios.get('https://themealdb.com/api/json/v1/1/search.php?s=' + this.search)
                .then((res) => {
                    this.meals = res.data.meals;
                })
                .catch((err) => {
                    console.log(err);
                });
            } else {
                swal({
                    title: "Atención",
                    text: "Debes de ingresar un texto",
                    icon: "error",
                });
            }
        },
        prev(){
            this.current--;
        },
        next(){
            this.current++;
        },
    },
};
</script>