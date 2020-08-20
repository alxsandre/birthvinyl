<template lang="html">

  <div class="container" v-on:keypress="goVynilEnter">
    <h1> BirthVynil</h1>
    <div class="block">
    <label for="date" class="contourVynil">


    <div class="centreVynil" >

      <div class="annee">
         Birth year :
      </div>
    <input id="date" type="number" min="1900" max="2021" placeholder="e.g. 1992" v-model="requete">
    </div>
    </label>
    </div>

    <div class="block">

    <selected>    </selected>
    <button class="search" v-on:click="goVynil"> search </button>

    </div>


    <div class="mise_enpage">

          <a :href="urlDiscogs + vynil.uri" target="_blank" v-for="vynil in vynile" :key="vynil.title" class="rendu">

                        <h2 > {{ vynil.title }} </h2>
                        <p class="year_rendu"> {{ vynil.year }}</p>
                        <img :src="vynil.cover_image" >

          </a>
    </div>





  </div>
</template>

<script>

import axios from 'axios'
import selected from './selected.vue'


export default {
  data(){
    return {
      requete: '',
      vynile : undefined,
      urlImg : undefined,
      urlLink : undefined,
      urlDiscogs : 'https://www.discogs.com/',
      key: 'UPWXwgmjADyNPEorXQBu',
      secret: 'XCzDtuTUPOWggbxSPWIJPLOOZtURodZP',
      url_recherche: 'https://api.discogs.com/database/search?'
    }
  },
  components: {
    'selected' : selected
  },
  methods: {
    goVynilEnter(e){
        if(e.key == "Enter"){
            this.goVynil()
        }
      },
    goVynil: function(){
      axios
        .get(`${this.url_recherche}genre=${this.$store.state.choisi[0]}&style=${this.$store.state.choisi[1]}&year=${this.requete}&format=album&type=master&key=${this.key}&secret=${this.secret}`)
        .then(response => {
          this.vynile = response.data.results
        })
        this.requete = ''
      }
    }
  }
</script>











<style >
.container{
  color : blue;
  display: flex;
  flex-direction: column;
  align-items: center;
}

h1{
  font-size: 8vw;
}



.rendu{
  margin : 4vw;
  border: solid 2px blue;
  font-size: 2vw;
  text-decoration: none;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  width: 40%;


  flex-wrap: nowrap;
}

a{
  text-decoration: none;
}

img{
  width: 100%;
  position: relative;

  border-top: solid 2px blue;

  margin: 0;
}

.year_rendu{
  font-size: 2.5vw;
  margin: 0.2vw;
  color: blue;

  position: relative;
  width: 100%;
  text-align: right;
  padding-right:10px;
  box-sizing: border-box;

}

h2{
  margin: 1vw;
  color: blue;
  text-align: center;

}



.contourVynil{
  margin: 1vw;
  border: 2px solid blue;
  border-radius: 100%;

  width: 60vw;
  height: 60vw;
  transition: background-color 500ms;
  display: flex;
  align-items: center;
  justify-content: center;
}


.centreVynil{
  background-color: blue;
  border: 2px solid blue;
  border-radius: 100%;
  width: 25vw;
  height: 25vw;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  cursor: pointer;
}


.annee{
  font-size: 2.5vw;
  color: white;
}

input{
  margin: 1vw;
  border: 0px;
  text-align: center;
  color: white;
  font-family: 'Montserrat', sans-serif;
  font-size: 2.5vw;
  outline: none;
  padding: .5rem;
  width: 70%;
  transition: background-color 500ms;
  background-color: blue;


}


.centreVynil:hover{
  border: 4px solid blue;
}

.centreVynil:focus{
  border: 4px solid blue;
}



input:not(:focus):invalid{
  background-color: red;
}


::-webkit-input-placeholder { /* WebKit browsers */
    color:    white;
    opacity:  0.4;
}
:-moz-placeholder { /* Mozilla Firefox 4 to 18 */
   color:    white;
   opacity:  0.4;
}
::-moz-placeholder { /* Mozilla Firefox 19+ */
   color:    white;
   opacity:  0.4;
}
:-ms-input-placeholder { /* Internet Explorer 10+ */
   color:   white;
   opacity:  0.4;
}

body{
  font-family: 'Montserrat', sans-serif;
}

.block{
  display: flex;
  justify-content: center;
  align-items: center;
}

.search{
  margin-left: 5vw;
  width: 10vw;
  height: 10vw;
  border-radius: 100%;
  background-color: white;
  border: 2px solid blue;
  color: blue;
  font-size: 2.5vw;
  text-align: center;
  cursor: pointer;
  outline: none;

 /*border-left: 10vw solid #ebdfca;
  border-right: 10vw solid transparent;
  border-bottom: 5vw solid transparent;
  border-top: 5vw solid transparent;
  */
}

.mise_enpage{
  display: flex;
  flex-wrap: wrap;
  width: 100%;
}

</style>
