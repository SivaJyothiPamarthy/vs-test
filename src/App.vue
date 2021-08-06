<template>
  <div id="app">
    <header>
      <h1>Image Finder</h1>
    </header>
    <div>
      <ImagesSearch v-model="authorNameSearch"></ImagesSearch>
      <pagination 
          :total-pages="totalPages"
          :per-page="perPage"
          :currentPage="currentPage"
          @pagechanged="onPageChange">
          
      </pagination>
    </div>
      <div class="cards">
          <ImagesList 
            v-for="content in filterImages"
            :key="content.id"
            :content="content"
          />
      </div> 
    
  </div>
</template>

<script>
  import axios from "axios";
  import ImagesList from './components/ImagesList';
  import ImagesSearch from './components/ImagesSearch';
  import Pagination from './components/Pagination';
  export default {
    name: 'App',
    components: {
      ImagesList,
      ImagesSearch,
      Pagination
    },
    data () {
      return {
        authorNameSearch: "",
        contents: null,
        currentPage: 1,
        totalPages: 34,
        perPage: 40
      }
    },
    async mounted () {
      const response = await axios.get('https://picsum.photos/v2/list?page=' + this.currentPage + '&?limit='+ this.perPage);
      if(response != undefined) {
        this.contents = response.data;
      }
    },
    computed: {
      filterImages: function() {
        let pictures = this.contents;
        let authorName = this.authorNameSearch;
        
        if(!authorName) {
          return pictures;
        }

        let searchString = authorName.trim().toLowerCase();
        pictures = pictures.filter(item => {
          if(item.author.toLowerCase().indexOf(searchString) !== -1) {
            return item;
          }
        })
        return pictures;
      }
    },
    methods: {
      async onPageChange(page) {
        this.currentPage = page;
        let response = await axios.get('https://picsum.photos/v2/list?page=' + this.currentPage + '&?limit='+ this.perPage)
        if(response != undefined) {
          this.contents = response.data;
        }
      }
    }
  };
</script>

<style>
  * {
    box-sizing: border-box;
    margin: 0;
    padding: 0;
  }

  html {
    overflow-y:scroll;
  }

  body {
    background-color: #f5f5f5;
    font-family: 'montseratt', sans-serif;
    margin-bottom: 20px;
  }

  header {
    display: grid;
    color: white;
    background: #5cbc25;
    padding: 20px;
  }

  header h1 {
    place-self: center;
    font-size: 40px;
  }

  .cards {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(367px, 1fr ));
    grid-gap: 30px;
    align-items: center;
    font-family: sans-serif;
  }
  
</style>
