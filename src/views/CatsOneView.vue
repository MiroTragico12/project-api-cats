<template>
    <div class="about">
      <div class="cards-container">
        <CardsComponents :cats="cats" />
      </div>
      <div id="paginacao">
        <router-link class="paginacao-button" to="/cats">1</router-link> 
        <router-link class="paginacao-button" to="/catsOne">2</router-link>
        <router-link class="paginacao-button" to="/catsTwo">3</router-link>
      </div>
    </div>
  </template>
  
  <script>
  import { getCats } from "../services/HttpService.js";
  import CardsComponents from "../components/CardsComponents.vue";
  
  export default {
    name: "CatsOneView",
    data() {
      return {
        cats: [],
      };
    },
    components: {
      CardsComponents,
    },
    methods: {
      async getCat() {
        try {
          const response = await getCats();
          this.cats = response.data;
        } catch (error) {
          console.error("Error fetching cats:", error);
        }
      },
    },
    created() {
      this.getCat();
    },
  };
  </script>
  
  <style scoped>
  .cards-container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
  }

  .paginacao-button{
    
    height: 30px;
    width: 50px;
    margin-right: 10px;
    margin-left: 10px;
    display: flex;
    justify-content: center;
    align-items: center;
    text-decoration: none;
    
    box-shadow: 0 2px 5px #aaa;
    border-radius: 10px;
    color: #000;
  }

  h1{
  text-align: center;
}

  #paginacao{
    display: flex;
    flex-direction: row;
    margin-top: 30px;
    align-items: center;
    justify-content: center;
  }

  #paginacao-button:hoover{
    background-color: #999;
    transform: .5s;
    cursor: pointer;
  }


  </style>
  