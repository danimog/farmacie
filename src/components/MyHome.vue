<template>
    <div class="container">
        <h1 class="title is-1 center">VUE3 - App Farmacie</h1>
        <button @click="onChange()">Go!</button>
        <hr>
        <span v-for="r in res.results" :key="r.cdAggregazione">
          {{r.city}} - {{r.address}} +-+ <span v-if="r.openings">{{r.openings.state}}</span> <br>
        </span>
        
    </div>
</template>

<script>
 import { ref } from "vue";

export default {
  setup() {
    const res = ref("");

    async function onChange() {
        // console.log("Stazione selezionata: "+stazione.value);
        // console.log("ciao")
        const PROXY = window.location.hostname === "localhost"
            ? "https://cors-anywhere.herokuapp.com"
            : "/cors-proxy";

        // const now = Date.now();
        // const nowgmt = new Date(now);
        
        const API_URL = 'https://m.paginegialle.it/mwrapper/searchpg?pagesize=20&output=json&lang=it&what=Farmacie+di+turno&autoc=1&where=Vernazza';
        const response = await fetch(`${PROXY}/`+API_URL).then(response => response.json())
        // const risultati = await response.then(res => res.json())

        console.log(response)

        res.value = response;
        console.log(res);
        // itemStazione.value = risultati;
        // console.log(itemStazione.value)
    }
    return { onChange, res };
  }

}
</script>

<style lang="scss" scoped>

</style>