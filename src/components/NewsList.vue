<template>

<ul >
  <div class="collection">
    <li v-for="article in articles">
    <div class="info">
      <div  class="photo">
          <img :src="article.urlToImage">
        </div>
      <div class="text">
        <div class="title">
          {{article.title }}
        </div>
        <div class="descript">
          {{article.description}}
        </div>
      </div>
    </div>
     
   </li>
  </div> 
</ul> 
<form submit.prevent="searchNews" class="d-flex flex-column justify-content-center">
    <div class="input-group mx-sm-3 mb-2"> 
      <label class="visually-hidden" for="search">Search</label>
      <input type="search" name="search" v-model="searchTerm" id="search" class="form-control mb-2 mr-sm-2" placeholder="Enter search term here" />
      <button class="btn btn-primary mb-2">Search</button>
    </div>
    <p>You are searching for {{ searchTerm }}</p>
 </form>

</template>

<script>
export default {
 data() {
 return {
     articles: [],
     searchTerm: ''
 }
 },
 methods: {
 searchNews() {
 let self = this;
 fetch('https://newsapi.org/v2/everything?q='+ 
self.searchTerm + '&language=en', {
 headers: {'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`,}
})
 .then(function(response) {
 return response.json();
 })
 .then(function(data) {
 console.log(data);
 self.articles = data.articles;
 });
 }
 },
   created() {
      let self = this;
      fetch('https://newsapi.org/v2/top-headlines?country=us', 
      {
    headers: {
    'Authorization': `Bearer ${import.meta.env.VITE_NEWSAPI_TOKEN}`}
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
  width:350px;
  height: 250px;
}
ul{
  list-style: none;
}


.collection 
{
  display: grid;
  grid-gap: 25px;
  grid-template-columns: repeat(3, 1fr);
}
.info{
   border-style: groove;
   border-color:grey ;
   border-bottom: 6px solid limegreen ;
}
.text{
  padding-top:10px;
}

</style>