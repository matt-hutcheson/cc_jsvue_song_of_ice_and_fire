<template lang='html'>
  <main>
    <div id="main-background">
      <h1>Game Of Thrones</h1>
      <great-houses :greatHouses='greatHouses'></great-houses>
      <article id='content-columns'>
        <characters-list v-if="characters.length" :characters='characters' :selectedHouse='selectedGreatHouse'></characters-list>
        <character-details v-if="selectedCharacter" :character="selectedCharacter"></character-details>
        <houses-list v-if="houses.length" :houses='houses' :selectedHouse='selectedGreatHouse'></houses-list>
        <img v-if="selectedGreatHouse" src="" :alt="selectedGreatHouse.name">
      </article>
    </div>
  </main>
</template>

<script>
import greatHouses from './components/greatHouses.vue';
import charactersList from './components/charactersList.vue';
import housesList from './components/housesList.vue';
import characterDetails from './components/characterDetails'
import {eventBus} from './main.js'

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
      characters: [],
      houses: [],

      arrynCheck: false,
      baratheonCheck: false,
      greyjoyCheck: false,
      lannisterCheck: false,
      martellCheck: false,
      starkCheck: false,
      tullyCheck: false,
      tyrellCheck: false,
    }
  },
  mounted () {
    this.getAllCharacters();
    this.getAllHouses();
    eventBus.$on('great-house-selected', (house) => {
      this.selectedGreatHouse = house
      this.characters = []
      this.houses = []
      this.getCharactersOfGreatHouse()
      this.getHousesOfGreatHouse()
    })
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
        .then(jresult => {for (const jhouse of jresult) {jhouse.id = this.getEndOfUrl(jhouse.url); this.gotHouses.push(jhouse); this.checkIfGreatHouse(jhouse)}})
        .then(() => this.gotHouses.sort(this.sortAlphabetical))
        .then(() => this.greatHouses.sort(this.sortAlphabetical))
      }
    },
    checkIfGreatHouse: function (house) {
      if (house.name === "House Arryn of the Eyrie" && !this.arrynCheck) {
        this.greatHouses.push(house)
        this.arrynCheck = true
      } else if (house.name === "House Baratheon of Dragonstone" && !this.baratheonCheck) {
        this.greatHouses.push(house)
        this.baratheonCheck = true
      } else if (house.name === "House Greyjoy of Pyke" && !this.greyjoyCheck) {
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
    },
    getCharactersOfGreatHouse: function () {
      for (const character of this.gotCharacters) {
        if (character.allegiances.length) {
          for (const houseUrl of character.allegiances) {
            if (houseUrl === this.selectedGreatHouse.url) {
              this.characters.push(character)
            }
          }
        }
      }
    },
    getHousesOfGreatHouse: function () {
      for (const house of this.gotHouses) {
        if (house.overlord === this.selectedGreatHouse.url) {
          this.houses.push(house)
        }
      }
    }
  },
  components: {
    'great-houses': greatHouses,
    'characters-list': charactersList,
    'houses-list': housesList,
    'character-details': characterDetails
  }
}
</script>

<style lang='css'>
@font-face {
  font-family: "GoT";
  src: local("GoT"),
  url(./assets/fonts/Game_of_Thrones.ttf) format("truetype");
}

main {
  width: 100vw;
  min-height: 100vh;
  margin: 0;
  background-color: rgb(5, 4, 4);
  color: #e1eef6;
}

#main-background {
  width: 100vw;
  min-height: 100vh;
  background: url('./assets/images/GoT_crow_dragon_background.jpg') no-repeat center center fixed;
  background-size: cover
}

h1 {
  font-family: "GoT", Helvetica, Arial;
  font-size: xxx-large;
  text-align: center;
  text-shadow: 4px 0 0 #004e66, -4px 0 0 #004e66, 0 4px 0 #004e66, 0 -4px 0 #004e66, 1px 1px #004e66, -1px -1px 0 #004e66, 1px -1px 0 #004e66, -1px 1px 0 #004e66;
  margin-top: 0;
  padding: 1em;
}

#content-columns {
  display: grid;
  grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
}

</style>