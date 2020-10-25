<template>
  <article>
        <h2>{{character.name}} details</h2>
        <dl>
            <dt>Name:</dt>
            <dd>{{character.name}}</dd>
            <dt>Aliases:</dt>
            <dd v-for='(alias, index) in character.aliases' :key='index'>alias</dd>
        </dl>
  </article>
</template>

<script>

export default {
    data () {
        return {
            
        }
    },
    props: ['character']
}
</script>

<style>

</style>