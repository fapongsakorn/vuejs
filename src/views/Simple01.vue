<template>
  <div class="container text-center">
    <h1>Simple Page</h1>
    <h1 v-if="show">{{name}}</h1>
    <v-btn color="success" @click="show = !show">switch</v-btn>&nbsp;
    <v-btn color="success" @click="callAlert()">alert</v-btn>
     <v-row>
      <v-col cols="3" v-for="(item,index) in catlist" :key="index">
      <v-card width="350">
        <v-img :src="item.img"></v-img>
        <v-card-title primary-title>
          <span>{{item.name}}</span>
        </v-card-title>
        <v-btn color="info" @click="callAlertParam(item.name)">info</v-btn>
      </v-card>
      </v-col>
      <v-col cols="12">
        <v-text-field
          name="name"
          label="name"
          id="name"
          v-model="name"
        ></v-text-field>
         <v-btn color="info" @click="callAlertParam(name)">info</v-btn>
         <simcom :name= "name" @callAlert="callAlert"/>
         <v-btn color="warning" @click="callSim()">callsim</v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>
import simcom from '../components/SimpleComponent.vue'
import {EventBus } from '@/EventBus'
export default {
  components: {
    simcom
  },
  data() {
    return {
      name: 'Pongsakorn Arkasri',
      show: false,
      catlist: [
        {name:'แมวยืน',img: require('../assets/Profile.jpg')},
        {name:'แมวอ้วน',img:require('../assets/profile01.png')}
      ]
    }
  },
  mounted() {
    EventBus.$on('MainCallAlert', this.callAlert)
  },
  methods: {
    callSim () {
      EventBus.$emit('SimComCallAlert')
    },
    callAlert() {
      alert('โฮ่ง')
    },
  },
}
</script>

<style>

</style>