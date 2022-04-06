<template>
<div class="py-5">
    <div class="bg-custom text-center">
    <h1 class="text-3xl  uppercase">{{body.name}}</h1>
    <hr class="m-5">
    <h5>EXP : {{body.base_experience}}</h5>
    <h5>Height : {{body.height}}</h5>
    <div class="mx-auto w-1/12">
    <img v-bind:src="img" alt="">
    </div>
    <h1>Skill</h1>
    <ul class="" v-for="skill in body.moves" v-bind:key="skill">
        <div class="m-5">
        <li class="p-5 flex flex-col bg-red-500">{{skill.move.name}}</li>
        </div>
    </ul>
    </div>
</div>
</template>

<script>
export default {
    name:'Detail',
    components:{},
    data() {
        return{
            id: this.$route.params.id,
            body:{},
            img:''

        }
    },
    methods:{
        async fetchDetailPokemon() {
            const res = await fetch('https://pokeapi.co/api/v2/pokemon/' + this.id)
            const data = res.json()
            return data
        }
    },
    async created(){
        const data = await this.fetchDetailPokemon()
        this.body = data
        this.img = data.sprites.front_default
        
    }
}
</script>