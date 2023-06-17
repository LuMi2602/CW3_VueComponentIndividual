<template>
    <div>
      <h2>Lesson List</h2>
      <ul>
        <li v-for="lesson in lessons" :key="lesson.id">
          <span>{{ lesson.name }}</span>
          <button @click="addToCart(lesson)">Add to Cart</button>
        </li>
      </ul>
    </div>
  </template>
  
  <script>
  export default {
    props: {
      lessons: {
        type: Array,
        required: true,
      },
    },
    methods: {
      addToCart(lesson) {
        this.$emit('addLesson', lesson);
      },
    },
  };
  </script>
  