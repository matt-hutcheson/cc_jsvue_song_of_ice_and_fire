<template lang='html'>
  <main>
    <ul>
      <li v-for="(character,index) in gotCharacters" :key="index">
        {{character.name}}
      </li>
    </ul>
    <ul>
      <li v-for="(house,index) in gotHouses" :key="index">
        {{house.name}}
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
        .then(jresult => {for (const jcharacter of jresult) {if (jcharacter.name) {this.gotCharacters.push(jcharacter)}}})
        .then(() => this.gotCharacters.sort(this.sortAlphabetical));
      }
    },
    getAllHouses: function () {
      const pages = [...Array(10).keys()]
      pages.shift()
      for (const page of pages) {
        fetch(`https://www.anapioficeandfire.com/api/houses?page=${page}&pageSize=50`)
        .then(result => result.json())
        .then(jresult => {for (const jhouse of jresult) {this.gotHouses.push(jhouse)}})
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
        }
  }
}
</script>

<style lang='css' scoped>

</style>