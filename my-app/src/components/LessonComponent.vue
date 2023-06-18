<template>
  <div id="item">
    <h2>Lesson List</h2>
    <ul>
      <li v-for="lesson in lessons" :key="lesson.id">
        <img id="img" :src="lesson.Image" />
        <p>{{ lesson.Subject}}</p>
        <p>Location:{{ lesson.Location}}</p>
        <p>Price:{{ lesson.Price}}</p>
        <!-- <p>Available Space: {{ lesson.Space - cartCount(lesson.id) }}</p> -->
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
    cartCount(id) {
          let count = 0;
          for (let i = 0; i < this.cart.length; i++) {
         // console.log(this.cart, id, 'this is cart and id')
            if (this.cart[i] == id) {
              count++;
            }
          }
          // console.log(count, 'this is count.')
          return count;
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
      /* background-image: url(images/scl.jpg); */
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
