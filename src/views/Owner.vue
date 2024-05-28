<template>
    <div class="container">
      <v-row>
        <v-col cols="6">
          <h1 class="text-start"><v-icon size="50" color="orange"></v-icon> &nbsp;PRODUCT</h1>
        </v-col>
        <v-col cols="6" class="text-end">
          <v-btn color="primary" @click="toggleForm"><v-icon>mdi-plus</v-icon>NEW PRODUCT</v-btn>
        </v-col>
      </v-row>
      <br>
      <v-form v-if="showForm" @submit.prevent="isEditMode ? updateProduct() : postAddProduct()">
        <v-card class="container">
        <v-text-field label="Product Name" v-model="postAddProductData.product_name" required></v-text-field>
        <v-text-field label="Price" v-model="postAddProductData.price" required type="number"></v-text-field>
        <v-text-field label="Amount" v-model="postAddProductData.amount" required type="number"></v-text-field>
        <v-text-field label="Detail" v-model="postAddProductData.detail" required></v-text-field>
        <v-text-field label="Username" v-model="postAddProductData.username" required></v-text-field>
        <v-btn color="primary" type="submit">{{ isEditMode ? 'UPDATE' : 'SAVE' }}</v-btn> &nbsp;
        <v-btn color="warning" @click="resetForm()">CLEAR</v-btn>
        </v-card>
      </v-form>
  
      <v-dialog v-model="showBuyDialog">
        <v-card>
          <v-card-title>รายการสั่งซื้อ</v-card-title>
          <v-card-title>{{ selectedProduct.product_name }}</v-card-title>
          <v-card-subtitle><br>
            ราคา: {{ selectedProduct.price }} บาท <br>
            รายละเอียด : {{ selectedProduct.detailsailsail }}
          
          </v-card-subtitle>
          <v-card-text>
            <v-text-field v-model="username" label="ชื่อ"></v-text-field>
            <v-text-field v-model="amount" label="จำนวน" type="number"></v-text-field>
          </v-card-text>
          <v-card-actions>
            <v-btn color="orange" style="color:white" @click="saveOrder">BUY</v-btn>
            <v-btn color="red" style="color:white" @click="closeBuyDialog">Cancel</v-btn>
          </v-card-actions>
        </v-card>
      </v-dialog>
  
      <br>
      <v-row>
        <v-col cols="12" class="container" v-for="item in apidata" :key="item._id">
          <v-card class="mx-auto" cols="12">
            <v-card-text>
              <v-row>
                <v-col cols="8">
                  <v-row>
                    <v-col cols="4">
                      <v-img width="350" height="250" src="../assets/image.jpg"></v-img>
                    </v-col>
                    <v-col cols="8">
                      <v-card-text>
                        <p class="text-h4 text--primary mx-3">{{ item.product_name }}</p>
                        <p class="mx-3"><b>ราคา</b> {{ item.price }} <b>บาท</b></p>
                        <p class="mx-3"><b>จำนวน</b> {{ item.amount }}</p>
                        <div class="text--primary mx-3">
                          <p><b>รายละเอียด</b></p>
                          {{ item.detail }}
                        </div>
                      </v-card-text>
                    </v-col>
                  </v-row>
                </v-col>
                <v-col cols="4" class="text-end">
                  <v-card-text>
                    <v-btn text color="deep-purple accent-4" @click="editProduct(item)">EDIT</v-btn>
                    &nbsp;
                    <v-btn text class="red" color="white accent-4" @click="deleteProduct(item._id)">DELETE</v-btn>
                    <br><br><br><br><br><br><br><br>
                    <!-- <v-btn width="150" text class="orange" color="white accent-4" @click="postAddOrder(item._id)"><v-icon size="20">mdi-cart-outline</v-icon>&nbsp;<b>BUY</b></v-btn> -->
                  </v-card-text>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
      <v-snackbar v-model="snackbar.show" :color="snackbar.color" top right>
        {{ snackbar.text }}
        <v-btn text @click="snackbar.show = false">Close</v-btn>
      </v-snackbar>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        apidata: [],
        showForm: false,
        isEditMode: false,
        postAddProductData: {
          _id: '',
          username: '',
          product_name: '',
          price: '',
          amount: '',
          detail: ''
        },
        snackbar: {
          show: false,
          text: '',
          color: ''
        },
        showBuyDialog: false,
        username: '',
        amount: 1,
        selectedProduct: {}
      };
    },
    created() {
      this.getData();
    },
    methods: {
      getData() {
        this.axios
          .get('http://localhost:3000/products/api/v1/product')
          .then(response => {
            console.log(response);
            this.apidata = response.data.product;
          })
          .catch(error => {
            console.error('Error fetching data:', error);
          });
      },
      postAddProduct() {
        console.log('Posting data:', this.postAddProductData);
        this.axios
          .post('http://localhost:3000/products/api/v1/product', this.postAddProductData)
          .then(response => {
            console.log(response);
            this.getData(); // Refresh the data
            this.resetForm();
            this.toggleForm();
            this.showSnackbar('Product added successfully!', 'success');
          })
          .catch(error => {
            console.error('Error posting data:', error);
            console.error('Error response data:', error.response.data);
            this.showSnackbar('Failed to add product.', 'error');
          });
      },
      postAddOrder(productId) {
        const product = this.apidata.find(item => item._id === productId);
        this.selectedProduct = { ...product };
        this.showBuyDialog = true;
      },
      saveOrder() {
        const orderData = {
          username: this.username,
          amount: this.amount
        };
        this.axios
          .post(`http://localhost:3000/orders/api/v1/product/${this.selectedProduct._id}/order`, orderData)
          .then(response => {
            console.log(response);
            this.getData(); // Refresh the data
            this.showSnackbar('Order placed successfully!', 'success');
            this.closeBuyDialog(); // Close the dialog after successful order
          })
          .catch(error => {
            console.error('Error saving order:', error);
            this.showSnackbar('Failed to place order.', 'error');
          });
      },
      editProduct(item) {
        this.postAddProductData = { ...item }; // Clone the item into postAddProductData
        this.isEditMode = true;
        this.showForm = true;
      },
      updateProduct() {
        console.log('Updating data:', this.postAddProductData);
        this.axios
          .put(`http://localhost:3000/products/api/v1/product/${this.postAddProductData._id}`, this.postAddProductData)
          .then(response => {
            console.log(response);
            this.getData(); // Refresh the data
            this.resetForm();
            this.toggleForm();
            this.showSnackbar('Product updated successfully!', 'success');
          })
          .catch(error => {
            console.error('Error updating data:', error);
            console.error('Error response data:', error.response.data);
            this.showSnackbar('Failed to update product.', 'error');
          });
      },
      deleteProduct(id) {
        this.axios
          .delete(`http://localhost:3000/products/api/v1/product/${id}`)
          .then(response => {
            console.log(response);
            this.getData(); // Refresh the data
            this.showSnackbar('Product deleted successfully!', 'success');
          })
          .catch(error => {
            console.error('Error deleting data:', error);
            this.showSnackbar('Failed to delete product.', 'error');
          });
      },
      toggleForm() {
        this.showForm = !this.showForm;
        if (!this.showForm) {
          this.resetForm();
        }
      },
      resetForm() {
        this.postAddProductData = {
          _id: '',
          username: '',
          product_name: '',
          price: '',
          detail: '',
          amount: ''
        };
        this.isEditMode = false;
      },
      closeBuyDialog() {
        this.showBuyDialog = false;
        this.username = '';
        this.amount = 1;
      },
      showSnackbar(message, color) {
        this.snackbar.text = message;
        this.snackbar.color = color;
          this.snackbar.show = true;
        }
      }
    };
    </script>
    
    <style>
    /* Add any necessary styles here */
    </style>
    