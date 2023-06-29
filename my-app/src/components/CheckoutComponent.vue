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
      <button id="submit" v-on:click="submitForm" :disabled="isButtonDisabled">Place Order</button>
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

    methods: {
      removeFromCart(lesson) {
        this.$emit('removeLesson', lesson);
      },
      submitForm() {
          let data = {}
            for (let i = 0; i < this.cart.length; i++) {
                const item = this.cart[i];
                if (!data[`${item["_id"]}`]) {
                    data[`${item["_id"]}`] = {
                        "spaces":1,
                        "item":item
                    }
                }else{
                    data[`${item["_id"]}`]["spaces"]++
                }
            }
            const keys = Object.keys(data)
            const values = Object.values(data)
            fetch(`http://localhost:3000/order`,{
                method:'POST',
                headers: {
                    'Content-Type': 'application/json'
                },
                body: JSON.stringify({
                    "name":this.inputl,
                    "phoneNumber":this.Inputn,
                })
            })
            .then(result => result.json())
            .then(result =>{
              console.log(result);
                    fetch(`http://localhost:3000/order/${result}`,{
                        method:'PUT',
                        headers: {
                            'Content-Type': 'application/json'
                        },
                        body: JSON.stringify({"items":values})
                    }).then(result => result.json())
                    .then(result => {
                            for (let i = 0; i < keys.length; i++) {
                                const key = keys[i];
                                const value = values[i];
                                console.log(value);
                                fetch(`http://localhost:3000/lesson/${key}`,{
                                    method:'PUT',
                                    headers: {
                                        'Content-Type': 'application/json'
                                    },
                                    body: JSON.stringify({"space":value["item"].Space})
                                })
                            }
                            this.cart = []
                            this.showCheckout()
                        
                    })
            }).catch(err =>{
                console.log(err);
            });
          alert('Order submitted!')

        },
    },
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
