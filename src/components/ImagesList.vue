<template>
    <div class="card">
      <img :src='"https://picsum.photos/id/" + content.id + "/367/267"' 
      class="card-img" alt="No image found"
      @click="iframeWin(content.url, content.id)">      
      <div class="card-content">
        <p class="card-text">{{content.author}}</p>
        <span class="card-id">{{content.id}}</span>
      </div>
    </div>
</template>

<script>
  export default {
    name: 'ImagesList',
    props:['content'],
    methods: {
      iframeWin(url) {
        const left = (screen.width / 5 ) ;
        const top = (screen.height ) ;
        window.open(url, "MsgWindow", "width=800,height=600,top="+ top + ", left=" + left);
      }
    }
}
</script>


<style scoped>
  
  .card {
    background: #EEE;
    border: none;
    box-shadow: 0px 0px 3px 0px rgba(0,0,0,0.1);
    border-radius: 10px;
    text-align: center;
    transition: transform .3s;
  }

  .card-img {
    width: 100%;
    display: block;
    border-top-left-radius: 20px;
    border-top-right-radius: 20px;
    cursor: pointer;
  }

  .card-content {
    display: flex;
    padding: 20px 10px;
    justify-content: space-between;
  }

  .card-text {
    text-overflow: ellipsis
  }

  @media (max-width: 768px){
    .cards {
      grid-template-columns: repeat(2, 1fr);
    }
  }

  @media (max-width: 500px) {
    .cards {
      grid-template-columns: repeat(1, 1fr);
    }
    .card {
      text-align: center;
    }
  }

</style>