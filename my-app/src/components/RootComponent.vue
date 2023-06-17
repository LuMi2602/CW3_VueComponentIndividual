
<template>
    <div>
      <h1>Lesson Store</h1>
      <button @click="toggleView">{{ getViewText() }}</button>
      <div v-if="view === 'lesson'">
        <LessonComponent :lessons="lessons" @addLesson="addToCart"></LessonComponent>
      </div>
      <div v-else>
        <CheckoutComponent :cart="cart" @removeLesson="removeFromCart"></CheckoutComponent>
      </div>
    </div>
  </template>
  
  <script>
  import LessonComponent from './LessonComponent.vue';
  import CheckoutComponent from './CheckoutComponent.vue';
  
  export default {
    name: 'RootComponent',
    components: {
      LessonComponent,
      CheckoutComponent,
    },
    data() {
      return {
        view: 'lesson',
        lessons: [],
        cart: [],
      };
    },
    methods: {
      toggleView() {
        this.view = this.view === 'lesson' ? 'checkout' : 'lesson';
      },
      getViewText() {
        return this.view === 'lesson' ? 'View Cart' : 'View Lessons';
      },
      addToCart(lesson) {
        this.cart.push(lesson);
      },
      removeFromCart(lesson) {
        const index = this.cart.findIndex((item) => item.id === lesson.id);
        if (index !== -1) {
          this.cart.splice(index, 1);
        }
      },
      fetchLessons() {
        fetch('http://localhost/lessons')
          .then(response => response.json())
          .then(data => {
            this.lessons = data;
          })
          .catch(error => {
            console.error(error);
          });
      },
    },
    mounted() {
      this.fetchLessons();
    },
  };
  </script>
  