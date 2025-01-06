<template>
    <h2 class="text-3xl font-bold mb-8">Favorites</h2>
    <FavoritList :products="favorites"/>
</template>

<script>
import axios from 'axios'
import FavoritList from '../components/ProductList.vue'

export default {
    components: {
        FavoritList
    },
    data: () => ({
        favorites: [],

    }),
    mounted() {

        this.getFavorites()
 
    },
    methods: {
        getFavorites(){
 
            try{
                axios.get(`https://67e54f4bc6572184.mokky.dev/favorites?_relations=products`)
                .then((response) => { 
                
                    console.log(response.data)
                    
                    this.favorites = response.data.map(this.setFavorite);
                    console.log(this.favorites)
                })
            } catch (error) {
                console.log(error);
            }
        },

        setFavorite(obj){
            obj.product.favoriteId = obj.id
            obj.product.isFavorite = true
            return (obj.product)
        }
    }
}
</script>