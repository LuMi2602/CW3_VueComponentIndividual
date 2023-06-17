<template>
    <div>
      <h2>Checkout</h2>
      <ul>
        <li v-for="lesson in cart" :key="lesson.id">
          <span>{{ lesson.name }}</span>
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
    },
    methods: {
      removeFromCart(lesson) {
        this.$emit('removeLesson', lesson);
      },
    },
  };
  </script>
  