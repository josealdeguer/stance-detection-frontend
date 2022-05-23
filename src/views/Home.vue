<template>
  <div class="container home">
    <v-layout row>
      <v-flex md6>
        <v-card shaped class="mx-auto" max-width="550">
          <v-img
           class="white--text align-end"
           height="350px"
           src="https://espacio-publico.com/wp-content/uploads/2019/02/desobediencia-catalu%C3%B1a-2.jpg"
           gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.2)"
          >
            <v-card-title class="headline font-weight-bold blue--text text--lighten-5">Independencia Cataluña</v-card-title>
          </v-img>
          <v-card-subtitle class="pb-0">Independencia de Catalañuna - El conflicto catalán</v-card-subtitle>
          <v-card-actions>
            <router-link :to="{ name: 'independencia' }">
              <v-btn color="blue" text>
                <v-icon>mdi-chart-line</v-icon>
                Analizar
              </v-btn>
            </router-link>
          </v-card-actions>
         </v-card>
      </v-flex>
      <v-flex md6>
        <v-card shaped class="mx-auto" max-width="550">
          <v-img
           class="white--text align-end"
           height="350px"
           src="https://www.publico.es/uploads/2020/04/25/5ea44127d3f8b.jpeg"
           gradient="to bottom, rgba(0,0,0,.1), rgba(0,0,0,.2)"
          >
            <v-card-title class="headline font-weight-bold blue--text text--lighten-5 ">Covid-19 España</v-card-title>
          </v-img>
          <v-card-subtitle class="pb-0">Gestión del Gobierno de España durante la crisis del Covid-19</v-card-subtitle>
          <v-card-actions>
            <router-link :to="{ name: 'coronavirus' }">
              <v-btn color="blue" text>
                <v-icon>mdi-chart-line</v-icon>
                Analizar
              </v-btn>
            </router-link>
          </v-card-actions>
         </v-card>
      </v-flex>
    </v-layout>

    <!-- <HelloWorld msg="Welcome to Your Vue.js App" /> -->
  </div>
</template>

<script>
// @ is an alias to /src
// import HelloWorld from "@/components/HelloWorld.vue";

export default {
  name: "Home",
  components: {
    // HelloWorld
  }
};
</script>

<style scoped>
.home {
  margin-top: 100px;
  max-width: 1200px;
}
a {
  text-decoration: none;
}
</style>
