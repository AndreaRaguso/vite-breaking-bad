<script>
export default {
    name: 'AppMain',
    props:{
        cardList:{
            type: Array,
            default: []
        }
    }
    
}
</script>

<template>
    
    <div class="container ">

        <div class="col-2 my-3">
            <select class="form-select" aria-label="Default select example">
                <option selected>Seleziona..</option>
                <option value="1">Alien</option>
                <option value="2">Melodious</option>
                <option value="3">Archfiend</option>
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
                            <div class="info p-3">
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