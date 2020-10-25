<template>
    <article v-if="selectedHouse">
        <h2>{{selectedHouse.name}} Details</h2>
        <dl>
            <dt>Name:</dt>
            <dd>{{selectedHouse.name}}</dd>
        </dl>
        <dl v-if="selectedHouse.region">
            <dt>Region:</dt>
            <dd>{{selectedHouse.region}}</dd>
        </dl>
        <dl v-if="selectedHouse.words">
            <dt>Words:</dt>
            <dd>{{selectedHouse.words}}</dd>
        </dl>
        <dl v-if="members.length">
            <dt>Members:</dt>
            <dd  v-for="(member, index) in members" :key="index">{{member.name}}</dd>
        </dl>
  </article>
</template>

<script>
import {eventBus} from '../main.js'
export default {
    name: 'house-details',
    props: ['characters'],
    data () {
        return {
            selectedHouse: null,
            founder: null,
            lord: null,
            heir: null,
            members: []
        }
    },
    mounted () {
        eventBus.$on('house-selected', (house) => {
            this.selectedHouse = house
            this.members = []
            this.getMembers()
    })
    },
    methods: {
        getFounder: function() {

        },
        getLord: function() {

        },
        getHeir: function() {

        },
        getMembers: function() {
            for (const character of this.characters) {
                if (character.allegiances.length) {
                    for (const house of character.allegiances) {
                        if (house === this.selectedHouse.url) {
                            this.members.push(character)
                        }
                    }
                }
            }
        }
    }

}
</script>

<style>

</style>