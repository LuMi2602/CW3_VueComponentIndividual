<template>
    <div>
      <h1>Lesson Store</h1>
      <button @click="toggleView">{{ getViewText() }}</button>
      <div v-if="view === 'lesson'">
        <LessonComponent :lessons="lessons" @addLesson="addToCart"></LessonComponent>
      </div>
      <div v-else>
        <CheckoutComponent :cart="cart" :cartCount="cartCount" @removeLesson="removeFromCart" @submitCart="submitCart"></CheckoutComponent>
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
    computed:{
      cartCount(){
        return `${this.cart.length}`
      }
    },
    methods: {
      submitCart(){
        alert("Order submited")
        this.cart = []
        this.toggleView()
      },
      toggleView() {
        this.view = this.view === 'lesson' ? 'checkout' : 'lesson';
      },
      getViewText() {
        return this.view === 'lesson' ? 'View Cart' : 'View Lessons';
      },
      addToCart(lesson) {
        lesson.Space--
        this.cart.push(lesson);
      },
      removeFromCart(lesson) {
        lesson.Space++
        const index = this.cart.findIndex((item) => item.id === lesson.id);
        if (index !== -1) {
          this.cart.splice(index, 1);
        }
      },
      fetchLessons() {
        fetch('http://localhost:3000/lesson')
          .then(response => response.json())
          .then(data => {
            this.lessons = data
          })
          .catch(error => {
            console.error(error);
          });
      },
    },
    created() {
      this.fetchLessons();
    },
  };
  </script>
  