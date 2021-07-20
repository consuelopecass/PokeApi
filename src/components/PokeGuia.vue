<template>
    <div>
        <img src="../assets/logoPokemon3.svg" alt="Logo Pokémon" width="400px">
        <h1>PokeGuía</h1>
        <form action="">
            <label for="">Ingresa tu Pokémon: </label>
            <input type="text" v-model="search">
            <input type="submit" @click.prevent="buscarPokemon" value="Buscar">
        </form>
        <section v-if="image !=''">
            <img :src="image" alt="Imagen Pokémon" width="180px">
            <h2>Nombre: {{name}}</h2>
            <h3>Habilidades</h3>
            <ul>
                <li v-for="ability in abilities" :key="ability">{{ability}}</li>
            </ul>
            <h3>Movimientos</h3>
            <ul>
                <li v-for="move in moves" :key="move">{{move}}</li>
            </ul>
        </section>
    </div>
</template>

<script>
export default {
    name: 'PokeGuia',
    //props
    data: function(){
        return {
            pokemon:{
                name: '', 
                sprite: '',
                moves: [],
                abilities: [],
            },
            search: 'pikachu'
        };
    },
    computed: {
        image(){
            return this.pokemon.sprite; 
        },
        name(){
            return this.pokemon.name; 
        },
        abilities(){
            let newList = [];
            this.pokemon.abilities.forEach((ability)=>{
                newList.push(ability.ability.name);
            });
            return newList;
        },
        moves(){
            let newList2 = [];
            this.pokemon.moves.forEach((move)=>{
                newList2.push(move.move.name);
            }); 
            return newList2;
        },
    }, 
    methods: {
        buscarPokemon(){
            //alert(this.pokemon.name); 
            fetch(`https://pokeapi.co/api/v2/pokemon/${this.search}`)
            .then(response => response.json())
            .then(json => {
                console.log(json)
                this.agregarPokemon(json)
            })
            .catch(error => {
                console.log('Este Pokémon no existe')
                console.log(error);
            });
        }, 
        agregarPokemon(json){
            let new_pokemon = {
                name: json.name,
                sprite: json.sprites.front_default,
                abilities: json.abilities,
                moves: json.moves,
        }; 
        this.pokemon = new_pokemon;
        },
    },
     // -- Lifecycle methods
    created(){
        this.buscarPokemon(); 
    },
    
}
</script>

<style scoped>
    * {
        margin: 0 auto;
        box-sizing: border-box;
        padding: 5px;
    }
    section {
        display: flex; 
        flex-direction: column;
        align-items: center;
    }
    h2, h3 {
        margin: 5px; 
    }
    li {
        list-style-type: none;
        margin: 0 auto; 
        padding: 5px; 
    }   
</style>