<template>
    <div class="container">
      <div class="calculator">
        <h1>Grade Calculator</h1><br>
        <div class="form-container">
          <input type="text" v-model="score" placeholder="Enter score">&nbsp;
          <v-btn class="primary" @click="calculateGrade"><v-icon class="sm">mdi-chevron-double-right</v-icon></v-btn>
        </div>
        <div v-if="grade" :class="['alert', 'alert-' + grade]">{{ grade }}</div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    data() {
      return {
        score: null,
        grade: null
      };
    },
    methods: {
      calculateGrade() {
        if (!this.score) {
          alert("Please enter a score.");
        } else if (this.score > 100 || this.score < 0 || isNaN(this.score)) {
          alert("Please enter a valid score between 0 and 100.");
          this.score = null; // Resetting the score
          this.grade = null;
        } else if (this.score >= 80 && this.score <= 100) {
          this.grade = "A";
        } else if (this.score >= 70 && this.score <= 79) {
          this.grade = "B";
        } else if (this.score >= 60 && this.score <= 69) {
          this.grade = "C";
        } else if (this.score >= 50 && this.score <= 59) {
          this.grade = "D";
        } else if (this.score >= 0 && this.score <= 49) {
          this.grade = "F";
        }
      }
    }
  };
  </script>
  
  <style scoped>
  .container {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100vh;
  }
  
  .calculator {
    text-align: center;
  }
  
  .form-container {
    border: 2px solid #ccc;
    border-radius: 10px;
    padding: 20px;
    margin-bottom: 20px;
  }
  
  .alert {
    margin-top: 10px;
    padding: 10px;
    border-radius: 5px;
  }
  
  .alert-A {
    background-color: #4caf50; /* Green */
    color: white;
  }
  
  .alert-B {
    background-color: #2196f3; /* Blue */
    color: white;
  }
  
  .alert-C {
    background-color: #ff9800; /* Orange */
    color: white;
  }
  
  .alert-D {
    background-color: #ff5722; /* Red */
    color: white;
  }
  
  .alert-F {
    background-color: #f44336; /* Dark Red */
    color: white;
  }
  </style>
  