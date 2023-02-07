<script>
import axios from 'axios';
import { store } from '../store.js';

export default {
    name: 'AppMain',
    data(){
        return{
            archetypes: [],
            selectedOption: 'Seleziona...',
            store
        }
    },
    methods:{
    
    },
    created() {
        this.store.loading = true;
        axios
            .get("https://db.ygoprodeck.com/api/v7/archetypes.php")
            .then((response) => {
                this.archetypes = response.data
                this.store.loading = false;
            });
    },
    computed:{
        onchange() {
            this.store.loading = true;
            axios
                .get("https://db.ygoprodeck.com/api/v7/cardinfo.php?archetype=" + this.selectedOption)
                .then((response) => {
                    this.store.card = response.data.data
                    this.store.loading = false;

                });
        }
    }
    
  }
</script>

<template>
    <!-- <button v-if="store.loading"  class="btn btn-primary" type="button" disabled>
        <span class="spinner-border spinner-border-sm" role="status" aria-hidden="true"></span>
        Loading...
    </button> -->
    <div class="container ">
        <div class="col-2 my-3">
            <select class="form-select" aria-label="Default select example" v-model="selectedOption" @change="onchange" >
                <option selected value="Seleziona...">Seleziona...</option>
                <option v-for="archetype in archetypes" :value="archetype.archetype_name">{{ archetype.archetype_name }}</option>
            </select>
        </div>
        <div class="bg-white">
            <div class="container py-5">
                <div class="bg-dark py-2">
                    <strong class="text-white mx-3">Found {{ store.card.length }} cards</strong> 
                </div>
                <div >
                    <div class="row">
                        <div class="col-2 mb-4" v-for="card in store.card">
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