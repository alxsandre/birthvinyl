<template lang="html">
  <div >


        <select v-model="$store.state.choisi" class="liste"  >
             <option value="">--Please choose a style--</option>
            <optgroup label="Electronic">
              <option v-for="musicElectro in musicElectros" v-bind:key="musicElectro.value" v-bind:value="musicElectro.value">
                {{ musicElectro.text }}
              </option>
            </optgroup>

            <optgroup label="Rock">
              <option v-for="musicRock in musicRocks" v-bind:key="musicRock.value" v-bind:value="musicRock.value">
                {{ musicRock.text }}
              </option>
            </optgroup>

              </select>



  </div>
</template>

<script>
export default {
  name: 'selected',
  data(){
    return {
  //   choisi: '',
     musicElectros: [
       { text: 'IDM', value: ["electronic","idm"] },
       { text: 'House', value: ["electronic","house"] },
       { text: 'Techno', value: ["electronic","techno"] }
     ],
     musicRocks:  [
       { text: 'Grunge', value: ["rock","grunge"] },
       { text: 'Pop Rock', value: ["rock","pop-rock"] },
       { text: 'Punk', value: ["rock","punk"] }
     ],
    }
  }
}
</script>

<style lang="css" scoped>


select{

  margin: 1vw;
  border: 2px solid blue;
  border-radius: 100rem;
  color: blue;
  font-family: 'Montserrat', sans-serif;
  font-size: 2.5vw;
  outline: none;
  padding: 1vw 2vw;

  transition: background-color 500ms;
}

option{
  text-align: center;
}



</style>
