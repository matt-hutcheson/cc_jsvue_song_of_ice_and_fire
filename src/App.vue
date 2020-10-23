<template lang='html'>
  <main>
    <ul>
      <li v-for="(character,index) in gotCharacters" v-if="character.name" :key="index">
        {{character.name}} {{character.id}}
      </li>
    </ul>
    <ul>
      <li v-for="(house,index) in gotHouses" :key="index">
        {{house.name}} {{house.id}}
      </li>
    </ul>
  </main>
</template>

<script>
export default {
  data () {
    return {
      gotCharacters: [],
      gotHouses: [],
      gotBooks: [],
      selectedCharacter: null
    }
  },
  mounted () {
    this.getAllCharacters();
    this.getAllHouses();
  },
  methods: {
    getAllCharacters: function () {
      const pages = [...Array(44).keys()]
      pages.shift()
      for (const page of pages) {
        fetch(`https://www.anapioficeandfire.com/api/characters?page=${page}&pageSize=50`)
        .then(result => result.json())
        .then(jresult => {for (const jcharacter of jresult) {jcharacter.id = this.getEndOfUrl(jcharacter.url); this.gotCharacters.push(jcharacter)}})
        .then(() => this.gotCharacters.sort(this.sortAlphabetical));
      }
    },
    getAllHouses: function () {
      const pages = [...Array(10).keys()]
      pages.shift()
      for (const page of pages) {
        fetch(`https://www.anapioficeandfire.com/api/houses?page=${page}&pageSize=50`)
        .then(result => result.json())
        .then(jresult => {for (const jhouse of jresult) {jhouse.id = this.getEndOfUrl(jhouse.url); this.gotHouses.push(jhouse)}})
        .then(() => this.gotHouses.sort(this.sortAlphabetical))
      }
    },
    sortAlphabetical: function(a,b) {
      const nameA = a.name.toUpperCase();
      const nameB = b.name.toUpperCase();
      if (nameA < nameB) {
        return -1;
      }
      if (nameA > nameB) {
        return 1;
      }
      return 0;
    },
    getEndOfUrl: function (url) {
      return Number(url.substr(url.lastIndexOf('/')+1));
    }

  }
}
</script>

<style lang='css' scoped>
main {
  width: 100vw;
  background-image: url(https://wallpaper-mania.com/wp-content/uploads/2018/09/High_resolution_wallpaper_background_ID_77702110892.jpg);
  display: grid;
  grid-template-columns: 1fr 1fr;
  color: #e1eef6;
}
</style>