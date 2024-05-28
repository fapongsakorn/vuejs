<template>
  <div class="container">
    <v-row>
        <v-col cols="12">
            <h1><v-icon size="50" color="orange">mdi-package-variant</v-icon> &nbsp;ORDER HERE</h1>
        </v-col>
    </v-row>
    <v-row>
      <!-- <h1>{{ apidata }}</h1> -->
        <v-col cols="12" v-for="item in apidata" :key="item._id">
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
                        <p class="mx-3"><b>ผู้ซื้อ:</b> {{ item.username }}</p>
                        <p class="mx-3"><b>ราคา:</b> {{ item.price }} <b>บาท</b></p>
                        <p class="mx-3"><b>จำนวน:</b> {{ item.amount }}</p>
                        <div class="text--primary mx-3">
                          <p><b>ราคารวม</b></p>
                          <h1>{{ item.totalprice }} THB.</h1>
                        </div>
                      </v-card-text>
                    </v-col>
                  </v-row>
                </v-col>
                <v-col cols="4" class="text-end">
                  <v-card-text>
                    <!-- <v-btn text color="deep-purple accent-4" @click="editProduct(item)">EDIT</v-btn> -->
                    &nbsp;
                    <v-btn text class="red" color="white accent-4" @click="deleteOrder(item._id)">DELETE</v-btn>
                  </v-card-text>
                </v-col>
              </v-row>
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
      <v-row>
        <v-col cols="12">
        <v-card>
          <v-row>
            <v-col cols="6" class="text-start">
              <v-card-title>TOTAL: {{ totalValue }} THB.</v-card-title>
              <!-- <v-divider></v-divider> -->
            </v-col>
            <v-col cols="6">
              <v-card-text class="text-end">
                <v-btn color="orange" width="150" style="color:white" @click="payNow">CHECK-OUT</v-btn>
              </v-card-text>
            </v-col>
          </v-row>
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
        snackbar: {
          show: false,
          text: '',
          color: ''
        }
      };
    },
    created() {
      this.getData();
    },
    methods: {
      getData() {
        this.axios
          .get('http://localhost:3000/orders/api/v1/order')
          .then(response => {
            console.log(response);
            this.apidata = response.data.orders;
            this.totalValue = response.data.totalValue;
          })
          .catch(error => {
            console.error('Error fetching data:', error);
          });
      },
      deleteOrder(id) {
        console.log(id)
        this.axios
          .delete(`http://localhost:3000/orders/api/v1/order/${id}`)
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
      showSnackbar(message, color) {
        this.snackbar.text = message;
        this.snackbar.color = color;
        this.snackbar.show = true;
      }
    }
}
</script>

<style>

</style>