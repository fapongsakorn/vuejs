<template>
  <v-container>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
          <v-btn terget="_blank" text href="/" >
              <h1 style="color:white">HOME</h1>
          </v-btn>
          <v-btn terget="_blank" text href="/search" >
              <b>SEARCH</b>
          </v-btn>
      </div>
      <v-spacer></v-spacer>
          <!-- <v-btn terget="_blank" text href="/" >  
              <b>GO SOMTING</b>
          </v-btn> -->
    </v-app-bar>
    <v-main>
      <router-view/>
    </v-main>
  </v-container>
</template>
<script>
export default {

}
</script>

<style>

</style>