<template>
  <div id="app">
    <h2>Lesson List</h2>
    <ul>
      <div>
          <h3>Sort:</h3>
          <input type="radio" id="subjectSort" value="subjectSort" v-model="sortOption" checked="true">
          <label for="subjectSort">Sort by Subject</label>
        </div>

        <div>
          <input type="radio" id="locationSort" value="locationSort" v-model="sortOption">
          <label for="locationSort">Sort by Location</label>
        </div>

        <div>
          <input type="radio" id="priceSort" value="priceSort" v-model="sortOption">
          <label for="priceSort">Sort by Price</label>
        </div>

        <div>
          <input type="radio" id="availabilitySort" value="availabilitySort" v-model="sortOption">
          <label for="availabilitySort">Sort by Availability</label>
        </div>

        <!--Code to allow the user to select where to arrange the items in ascending or 
            descending order-->
        <div>
          <h3>Order By:</h3>
          <input type="radio" id="asc" value="asc" v-model="sortOption">
          <label for="asc">Ascending order</label>
        </div>

        <div>
          <input type="radio" id="desc" value="desc" v-model="sortOption">
          <label for="desc">Descending Order</label>
        </div>

        <!-- searchbox -->
        <div id="searchinput">
          <input type="text" v-model="userSearch" @input="handleSearch" placeholder="Search">
          <label for="searchinput"><strong>Search</strong></label>
        </div>

        
        <!-- displaying results of the search  -->
        
        <div id="item" v-for="result in searchEmpty" :key="result._id">
          <img id="img" :src="result.images" />
          <p>{{ result.Subject }}</p>
          <p>Location: {{ result.Location }}</p>
          <p>Price: {{ result.Price }}</p>
          <p>Available Space: {{ result.Space }}</p>
          <button v-on:click="addToCart(result)" v-if="result.Space > 0">Add to cart</button>
          <button disabled="disabled" v-else>Add to cart</button>
        </div>

        <!--Displaying items sorted by order of Subject upon button selection-->
        <div v-if="sortOption === 'subjectSort'">
          <div id="item" v-for="x_classes in SubjectSort" :key="x_classes.id">
            <img id="img"><img v-bind:src="x_classes.images"/>
            <p v-text="x_classes.Subject"></p>
            <p>Location : {{x_classes.Location}}</p>
            <p>Price : {{x_classes.Price}}</p>
            <p>Available Space:{{ x_classes.Space}}</p>

            <button v-on:click='addToCart(x_classes)' v-if='result.Space > 0'>Add to cart</button>
            <button disabled="disabled" v-else>Add to cart</button>
          </div>


        </div>

        <!--Displaying items sorted by order of Location upon radio button selection-->
        <div v-if="sortOption == 'locationSort'">
          <div id="item" v-for=" x_classes in LocationSort" :key="x_classes.id">

            <img id="img"><img v-bind:src="x_classes.images"/>

            <p v-text="x_classes.Subject"></p>
            <p>Location : {{x_classes.Location}}</p>
            <p>Price : {{x_classes.Price}}</p>
            <p>Available Space:{{ x_classes.Space }}</p>

            <button v-on:click='addToCart(x_classes)' v-if='result.Space > 0'>Add to cart</button>
            <button disabled="disabled" v-else>Add to cart</button>


          </div>
        </div>
        <div id="item" v-for="lesson in lessons" :key="lesson.id">
        <img id="img" :src="lesson.images" />
        <p>{{ lesson.Subject}}</p>
        <p>Location:{{ lesson.Location}}</p>
        <p>Price:{{ lesson.Price}}</p>
        <p>Available Space: {{ lesson.Space }}</p>
        <button @click="addToCart(lesson)">Add to Cart</button>
        </div>
        
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
  created(){
    this.lessons_array = this.lessons
  },
  data(){
    return {
      sortOption: "subjectSort",
   userSearch: '',

searchEmpty: [],
lessons_array:[],
emptyCart: true,
    }

  },
  methods: {
    addToCart(lesson) {
      this.$emit('addLesson', lesson);
    
    },
    handleSearch() {
          if (this.userSearch.length > 0) {
            
            return this.searchEmpty = [...this.lessons].filter(item => {
              const RegX = new RegExp(this.userSearch, 'i')
              return RegX.test(item.Subject) || RegX.test(item.Location.toString())
            })

          } else {
            this.searchEmpty = []
          }
          
        },
  },
  watch:{
    handleSearch() {
      console.log(this.userSearch);

    },
  },
  computed:{
    
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
