<template>
    <div>
      <h2>Checkout</h2>
      <h3>count</h3>
      
      {{cartCount}}
      <ul>
        <li v-for="lesson in cart" :key="lesson._id">
          <img id="img" :src="lesson.images" />
        <p>{{ lesson.Subject}}</p>
        <p>Location:{{ lesson.Location}}</p>
        <p>Price:{{ lesson.Price}}</p>
          <button @click="removeFromCart(lesson)">Remove</button>
        </li>
      </ul>
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
    },
  };
  </script>
  