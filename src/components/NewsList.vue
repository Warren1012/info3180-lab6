<template>

<ul >
  <div class="collection">
    <li v-for="article in articles">
      <div  class="photo">
        <img :src="article.urlToImage">
      </div>
      <div class="info">
        {{article.title }}
        {{article.description}}
      </div>
   </li>
  </div> 
 </ul> 


</template>

<script>
export default {
 data() {
 return {
     articles: []
 }
 },
   created() {
      let self = this;
      fetch('https://newsapi.org/v2/top-headlines?country=us', 
      {
    headers: {
    'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}` 
      }
    })
    .then(function(response) {
    return response.json();
    })
    .then(function(data) {
    console.log(data);
    self.articles = data.articles;
    });
    }
};
</script>

<style>
  img{
  width:75%;
}
ul{
  list-style: none;
}
*{
  box-sizing: border-box;
}

.collection {
  display: grid;
  grid-auto-columns: max-content;
  grid-auto-flow: dense;
  grid-auto-rows: minmax(100px, auto);
  grid-gap: 25px;
  grid-template-columns: repeat(3, 1fr);
  
  margin: 60px auto;
  max-width: 800px;
  border: solid;
  border-color: aqua;
}

.info{
  padding-top: 10px;
}
.collection > div{
   background-color: #80cbc4;
  border: 1px solid #fff;
  padding: 40px;
  font-size: 30px;
  text-align: center;
}
</style>