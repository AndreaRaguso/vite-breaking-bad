<script>
import axios from 'axios';


export default {
    name: 'AppMain',
    data(){
        return{
            archetypes: [],
            link: '',
            selectedOption: ''
        }
    },
    props:{
        cardList:{
            type: Array,
            default: []
        },
    },
    methods:{
        ciao(value){
            console.log("pio",value)
        }
    },
    created() {
    this.link = "https://db.ygoprodeck.com/api/v7/archetypes.php"
        axios
            .get(this.link)
            .then((response) => {
                this.archetypes = response.data
            });
  },
    
  }
</script>

<template>
    
    <div class="container ">

        <div class="col-2 my-3">
            <select class="form-select" aria-label="Default select example" v-model="selectedOption">
                <option selected>Seleziona...</option>
                <option v-for="(archetype, index) in archetypes" :value="archetype.archetype_name" :key="index">{{ archetype.archetype_name }}</option>
             </select>
        </div>

        <div class="bg-white">

            <div class="container py-5">
                <div class="bg-dark py-2">
                    <strong class="text-white mx-3">Found {{ cardList.length }} cards</strong> 
                </div>
                <div >
                    <div class="row">
                        <div class="col-2 mb-4" v-for="card in cardList">
                            <div>
                                <img :src= "card.card_images[0].image_url" alt="" class=" img-fluid">
                            </div>
                            <div class="info p-3 d-flex flex-column  justify-content-between">
                                <h3 class="text-white"> {{ card.name }}</h3>
                                <h4 class="text-center">{{card.archetype}}</h4>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>

    </div>

</template>

<style lang="scss" scoped>
@import '../styles/partials/AppMain.scss';
</style>