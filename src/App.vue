<template lang='html'>
  <main>
    <great-houses :greatHouses='greatHouses'></great-houses>
    <section id='content-columns'>
      <characters-list :characters='gotCharacters'></characters-list>
      <houses-list :houses='gotHouses'></houses-list>
    </section>
  </main>
</template>

<script>
import charactersList from './components/charactersList.vue';
import housesList from './components/housesList.vue';
import greatHouses from './components/greatHouses.vue';

export default {
  name: 'App',
  data () {
    return {
      gotCharacters: [],
      gotHouses: [],
      gotBooks: [],
      greatHouses: [],
      selectedCharacter: null,
      selectedHouse: null,
      selectedGreatHouse: null,
      arrynCheck: false,
      baratheonCheck: false,
      greyjoyCheck: false,
      lannisterCheck: false,
      martellCheck: false,
      starkCheck: false,
      tullyCheck: false,
      tyrellCheck: false

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
    checkIfGreatHouse: function (house) {
      if (house.name === "House Arryn of the Eyrie" && !this.arrynCheck) {
        this.greatHouses.push(house)
        this.arrynCheck = true
      } else if (house.name === "House Baratheon of Dragonstone" && !this.baratheonCheck) {
        this.greatHouses.push(house)
        this.baratheonCheck = true
      } else if (house.name === "House Greyjoy of Pike" && !this.greyjoyCheck) {
        this.greatHouses.push(house)
        this.greyjoyCheck = true
      } else if (house.name === "House Lannister of Casterly Rock" && !this.lannisterCheck) {
        this.greatHouses.push(house)
        this.lannisterCheck = true
      } else if (house.name === "House Nymeros Martell of Sunspear" && !this.martellCheck) {
        this.greatHouses.push(house)
        this.martellCheck = true
      } else if (house.name === "House Stark of Winterfell" && !this.starkCheck) {
        this.greatHouses.push(house)
        this.starkCheck = true
      } else if (house.name === "House Tully of Riverrun" && !this.tullyCheck) {
        this.greatHouses.push(house)
        this.tullyCheck = true
      } else if (house.name === "House Tyrell of Highgarden" && !this.tyrellCheck) {
        this.greatHouses.push(house)
        this.tyrellCheck = true
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
  },
  components: {
  'characters-list': charactersList,
  'houses-list': housesList,
  'great-houses': greatHouses
  }
}
</script>

<style lang='css' scoped>
main {
  width: 100vw;
  background-image: url(https://wallpaper-mania.com/wp-content/uploads/2018/09/High_resolution_wallpaper_background_ID_77702110892.jpg);
  color: #e1eef6;
}

#content-columns {
  display: grid;
  grid-template-columns: 1fr 1fr;
}
</style>