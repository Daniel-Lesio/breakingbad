<template>
  <q-page class="row justify-center align-center q-pa-md items-center q-gutter-md">
    <q-card class="carta" v-for="(character ,index) in characters" :key="index"
    v-on:click='openModal(character)'
     >
      <q-card-section>
        {{  character.name}}
      </q-card-section>
      <q-card-section>
        <q-img :ratio="1"  class="img"  :src="character.img" alt=""/>
      </q-card-section>
      <q-btn  color="primary  q-ma-sm btn" text-color="black" label="More" />
    </q-card>
 <q-dialog
      v-model="modal"
      persistent
      :maximized="maximizedToggle"
      transition-show="slide-up"
      transition-hide="slide-down"
      row
      
    >
      <q-card class="bg-primary text-white text-center">
        <q-bar>
          <q-space />

          <q-btn dense flat icon="minimize" @click="maximizedToggle = false" :disable="!maximizedToggle">
            <q-tooltip v-if="maximizedToggle" content-class="bg-white text-primary">Minimize</q-tooltip>
          </q-btn>
          <q-btn dense flat icon="crop_square" @click="maximizedToggle = true" :disable="maximizedToggle">
            <q-tooltip v-if="!maximizedToggle" content-class="bg-white text-primary">Maximize</q-tooltip>
          </q-btn>
          <q-btn dense flat icon="close" v-close-popup>
            <q-tooltip content-class="bg-white text-primary">Close</q-tooltip>
          </q-btn>
        </q-bar>

        <q-card-section>
          <div class="text-h6">{{ modalName }}</div>
        </q-card-section>

        <q-card-section class="">
               <div class="person row ">
                 <q-img   class="img"  :src="modalImg" alt=""/>
               <div class="info">
                 <p class="q-ma-sm">birthday : {{ modalBirth }}</p>
                <p class="q-ma-sm"> nickname : {{ modalNick }} </p>
                <p class="q-ma-sm">Occupations</p>
                <ul class="lista">
                  <li v-for='(occupation,index) in modalOccupations' :key="index">
                    {{ occupation }}
                  </li>
                </ul>
                <p class="q-ma-sm">actor : {{ modalActor }}</p>
               </div>
               </div>
                <p class="q-ma-sm">Quotes : </p>
                <p class="quota q-ma-sm" v-for='(quote,index) in this.modalQuotes' :key='index' >
                  {{ quote.quote }}
                </p>
               
        </q-card-section>
      </q-card>
    </q-dialog>
  </q-page>
</template>

<script>
export default {
  data(){
    return{
      modal : false,
      modalImg : '',
      modalName : '',
      modalNick : "",
      modalQuotes : [],
      modalBirth : '',
      modalOccupations : [],
      modalActor : '',
      characters : [],
      quotes : [],
      maximizedToggle: true,

    }
  },
  async created(){
    let url = 'https://www.breakingbadapi.com/api/'
    const characters = await this.$axios.get(`${url}characters`)
    this.characters = characters.data
    const quotes = await this.$axios.get(`${url}quotes`)
    this.quotes = quotes.data
    console.log(this.quotes)
  },
  methods : {
    openModal(character){
      console.log(character)
      this.modalImg = character.img
      this.modalName = character.name
      this.modalNick = character.nickname
      this.modalBirth = character.birthday
      this.modalOccupations = character.occupation
      this.modalActor = character.portrayed
      const quoty = this.quotes.filter(quote=> quote.author == character.name )
      this.modalQuotes = quoty
      console.log(this.modalQuotes )
      this.modal = !this.modal 
      
    }
  }
}
</script>
<style lang="scss" scoped>
  .carta{
    background-color: $grey-5;
    width: 300px;
    max-width: 90%;
    margin-left: auto;
    margin-right: auto;
    display: flex;
    flex-direction: column;
    text-align: center;
    cursor: pointer;
    .img{
      object-fit:cover
    }
  }
  .btn{
    align-self: center!important;
    margin-left: auto;
    margin-right: auto;
    color: white!important;
    letter-spacing: 3px;
  }
  .modal{
    width: 90%!important;
  }
  .img{
    width: 300px;
    max-width: 90%;
  }
  .person{
    display: flex;
    justify-content: center;
    text-align: left;
    background-color: #3c3c3c;
    padding: 20px;
    .img{
      margin-right: 10px
    }
  }
  .lista{
    margin-top: 10px;
    margin-left: 30px;
    padding: 0;

    // list-style: none;
  }
  .quota{
    line-height: 50px;
    border: #ddd solid 1px;
    color: #ddd;
  }
</style>