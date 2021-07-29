<template>
  <div id="app">
      <button @click="getCharacters">Get 5 random characters!</button>
      <div v-for="(character, index) in characters" :key="index" class="character">
        <img :src="character.img" alt="">
        <h2>{{character.name}}</h2>
      </div>
  </div>
</template>

<script>

export default {
  name: "App",
  data:()=>{
    return {
      characters:[]
    }
  },
  async mounted() {
    let res = await fetch('https://rickandmortyapi.com/api/character/1,2,3,4,5')
    let data = await res.json()
    console.log(data)
    this.characters = data.map((character)=>{
      return {name: character.name, img: character.image}
    });
  },
  methods:{
    async getCharacters(){
      let numbers = []
      for(let i=0; i<5; i++){
        let n = Math.floor(Math.random() * 672);
        numbers.push(n);
      }
      let [n1, n2, n3, n4, n5] = numbers;
      let res = await fetch(`https://rickandmortyapi.com/api/character/${n1},${n2},${n3},${n4},${n5}`)
      let data = await res.json()
      this.characters = data.map((character)=>{
        return {name: character.name, img: character.image}
      })

    }
  }
  
};
</script>

<style lang="scss">
#app {
  font-family: 'Open Sans', sans-serif;
  color: white;
  width: 90%;
  margin: 60px auto;
  display: flex;
  flex-direction: column;
}
body{
  background-image:url("https://styledme.com/wp-content/uploads/2020/09/rick-and-morty-virtual-backgrounds-images-for-zoom-meetings.jpg");
  background-repeat: no-repeat;
}

button{
  align-self: center;
  margin-bottom: 3em;
  background: #6FC536;
  color: #fff;
  border: none;
  padding: 10px 20px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.character{
  display: flex;
  flex-wrap: wrap;
  font-size: 20px;
  align-items: center;
  margin-bottom: 2.5rem;
}
.character h2{
    position: relative;
    cursor: pointer;

}
.character h2::after{
  content: "";
  position: absolute;
  left: 0;
  top: 40px;
  width: 0%;
  height: 3px;
  background-color:  #6FC536;
}
.character h2:hover:after{
  width: 100%;
  transition: all .2s;
}
.character img{
  width: 7rem;
  border-radius: 100px;
  border:  #6FC536 2px solid;
  margin-right: 1em;
}

@media (max-width: 450px){
  .character{
    flex-direction: column;
  }
  body{
    background-size: cover;
  }
}
</style>
