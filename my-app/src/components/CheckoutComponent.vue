<template>
    <div>
      <h2>Checkout</h2>
      <h3>Cart</h3>
      {{cartCount}}

      <p>
          <strong>First Name:</strong>
          <input type="text" v-model="inputl" >
        </p>

        <p>
          <strong>Phone Number:</strong>
          <input type="text" v-model="Inputn">
        </p>
      
      <div id="item" v-for="lesson in cart" :key="lesson._id">
          <img id="img" :src="lesson.Image" />
        <p>{{ lesson.Subject}}</p>
        <p>Location:{{ lesson.Location}}</p>
        <p>Price:{{ lesson.Price}}</p>
          <button @click="removeFromCart(lesson)">Remove</button>
        
     </div>
     <div id="submit">
      <!-- <button v-on:click="submitForm">Place Order</button> -->
      <button id="submit" v-if="LetterMust && numberMust" v-on:click="submitForm" :disabled="isButtonDisabled">Place Order</button>
  </div>
    </div>
  </template>
  
  <script>

  export default {
    props: {
      cart: {
        type: Array,
        required: true,
      },
      cartCount: {
      type: String,
      required: false,
      },
    },
    emits:["submitCart"],
    data(){
      return {
        inputl: '',
         Inputn: '',
      }
    },
    methods: {
      removeFromCart(lesson) {
        this.$emit('removeLesson', lesson);
      },
      submitForm() {
        this.$emit('submitCart');

        },

    },

    computed:{
      numberMust() {
        let res = this.Inputn.match(/^[0-9]+$/)
      return res
   },

LetterMust() {
  let res = this.inputl.match(/^[a-zA-Z\s]+$/)
return res
}
    }
  };
  </script>
  
  <style>
    body {
      color: white;
      font-family: Arial, Helvetica, sans-serif
    }

    footer {

      color: white;
    }

    #app {
      /* background-image: url(public/assets/scl.png); */
      background-size: contain;
      padding-left: 1.5rem;

    }

    #item {

      text-decoration-color: white;
      background-color: #212142;
      max-width: 320px;
      margin-right: 3rem;
      margin-top: 1rem;

      margin-bottom: 3rem;
      padding: 1rem;
      border: 1px solid #212142;
      border-radius: 1rem;
      display: inline-block;

    }
    

    img {
      box-sizing: border-box;
      padding-left: 0%;
      object-fit: cover;
      width: 100%;
      text-decoration-color: aliceblue;

    }

    #searchinput {
      width: 40%;
      padding-left: 35%;
      margin-top: 1rem;


    }

    #submit {
      font-size: medium;
      position: relative;
      margin-bottom: 1rem;
    }
  </style>
