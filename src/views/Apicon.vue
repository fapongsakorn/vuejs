<template>
    <div class="container">
      <h1>API CONNECT</h1>
      <v-row>
        <v-col cols="2" v-for="(item, index) in apidata" :key="index">
          <v-card width="350">
            <v-img src="../assets/Profile.jpg"></v-img>
            <v-card-title primary-title>
              <span>
                Product Name: {{ item.product_name }} <br>
                Price: {{ item.price }} <br>
                Amount: {{ item.amount }} <br>
              </span>
            </v-card-title>
          </v-card>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12">
          <v-btn color="primary" @click="getData()">GET DATA</v-btn>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12">
          <v-btn color="primary" @click="toggleForm()">REGISTER NEW PRODUCT</v-btn>
        </v-col>
      </v-row>
      <v-row>
        <v-dialog v-model="dialogedit" max-width="500">
            <v-card>
                <v-card-title primary-title>
                    title
                </v-card-title>
                <v-card-text>
                    <v-row>
                        <v-col cols="12">
                            
                        </v-col>
                    </v-row>
                </v-card-text>
            </v-card>
        </v-dialog>
      </v-row>
      <v-form v-if="showForm" @submit.prevent="postRegister">
        <v-text-field label="Product Name" v-model="postRegisterData.product_name" required></v-text-field>
        <v-text-field label="Price" v-model="postRegisterData.price" required></v-text-field>
        <v-text-field label="Amount" v-model="postRegisterData.amount" required></v-text-field>
        <v-text-field label="Detail" v-model="postRegisterData.detail" required></v-text-field>
        <v-text-field label="Username" v-model="postRegisterData.username" required></v-text-field>
        <v-btn color="primary" @click="postRegister()" type="submit">SAVE</v-btn>
      </v-form>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        apidata: [],
        showForm: false,
        postRegisterData: {
          username: '',
          product_name: '',
          price: '',
          amount: '',
          detail: '',
        }
      }
    },
    methods: {
      getData() {
        this.axios.get('http://localhost:3000/products/api/v1/product')
          .then((response) => {
            console.log(response)
            this.apidata = response.data.product
          })
          .catch((error) => {
            console.error('Error fetching data:', error)
          })
      },
      postRegister() {
        console.log('Posting data:', this.postRegisterData) // Log the data to be posted
        this.axios.post('http://localhost:3000/products/api/v1/product', this.postRegisterData)
          .then((response) => {
            console.log(response)
            this.getData() // Refresh the data
            this.resetForm()
            this.toggleForm()
          })
          .catch((error) => {
            console.error('Error posting data:', error)
            console.error('Error response data:', error.response.data) // Log the response data from the error
          })
      },
      toggleForm() {
        this.showForm = !this.showForm
      },
      resetForm() {
        this.postRegisterData = {
          username: '',
          product_name: '',
          price: '',
          detail:'',
          amount: ''
        }
      }
    }
  }
  </script>
  
  <style>
  /* Add any necessary styles here */
  </style>
  