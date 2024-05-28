<template>
  <div>
    <v-app-bar
      app
      color="dark"
      dark
    >
      <div class="d-flex align-center">
          <v-btn terget="_blank" text href="/me" >
              <h1 style="color:orange">HOME</h1>
          </v-btn>
          <v-btn terget="_blank" text href="/simple" >
              <b>SIMPLE</b>
          </v-btn>
          <v-btn terget="_blank" text href="/grade" >
              <b>GRADE</b>
          </v-btn>
          
          <v-btn terget="_blank" text href="/apicon" >
              <b>GETAPI</b>
          </v-btn>
      </div>
      <v-spacer></v-spacer>
           <v-btn terget="_blank" text href="/shopping" >
              <b>SHOP</b>
          </v-btn>
          <v-btn terget="_blank" text href="/owner" >
              <b>OWNER</b>
          </v-btn>
          <v-btn terget="_blank" text href="/order" >
              <b><v-icon size="35" color="orange">mdi-package-variant</v-icon></b>
          </v-btn>
         
    </v-app-bar>
    <v-main>
      <router-view/>
    </v-main>
  </div>
</template>
<script>
export default {

}
</script>

<style>

</style>