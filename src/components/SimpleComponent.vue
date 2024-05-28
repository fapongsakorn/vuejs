<template>
  <div class="container">
    <h1>Simple Components</h1>
    <h2>{{ name }}</h2>
    <v-btn color="primary" @click="callMain()">callMain</v-btn>
  </div>
</template>

<script>
import {EventBus } from '@/EventBus'
export default {
    props: ['name'],
    mounted(){
        EventBus.$on('SimComCallAlert', this.SimComAlert)
    },
    methods: {
       callMain(){
        EventBus.$emit('MainCallAlert')
       },
       SimComAlert(){
        alert("เหมียว")
       }
    },
}
</script>

<style>

</style>