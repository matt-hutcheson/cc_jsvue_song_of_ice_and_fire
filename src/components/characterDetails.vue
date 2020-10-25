<template>
  <article>
        <h2>{{character.name}} details</h2>
        <dl>
            <dt>Name:</dt>
            <dd>{{character.name}}</dd>
        </dl>
        <dl v-if='character.aliases[0] != ""'>
            <dt >Aliases:</dt>
            <dd v-for='(alias, index) in character.aliases' :key='index'>{{alias}}</dd>
        </dl>
        <dl v-if='character.titles[0] != ""'>
            <dt >Titles:</dt>
            <dd v-for='(title,index) in character.titles' :key='index'>{{title}}</dd>
        </dl>
        <dl v-if='character.culture != ""'>
            <dt >Culture:</dt>
            <dd>{{character.culture}}</dd>
        </dl>
        <dl v-if='character.gender != ""'>
            <dt >Gender:</dt>
            <dd>{{character.gender}}</dd>
        </dl>
        <dl v-if='character.born != ""'>
            <dt >Born:</dt>
            <dd>{{character.born}}</dd>
        </dl>
        <dl v-if='character.playedBy[0] != ""'>
            <dt >Played By:</dt>
            <dd v-for='(playedBy,index) in character.playedBy' :key='index'>{{playedBy}}</dd>
        </dl>
  </article>
</template>

<script>

export default {
    name: 'character-details',
    data () {
        return {
            
        }
    },
    props: ['character']
}
</script>

<style scoped>
    
</style>