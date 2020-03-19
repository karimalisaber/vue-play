<template>
<div class ="main-item container">
  <ul>
  <li> Hello <span> {{this.$route.query.name}} </span> </li> 
  <li> your email is <span>  {{this.$route.query.email}} </span> </li> 
  <li> it's a 1k rows random data for You </li> 
</ul>

  <v-data-table
    :headers="posts.headers"
    :items="posts.desserts"
    :items-per-page="10"
    class="elevation-1"
  ></v-data-table>
</div>
  
</template>

<script lang="ts">
import Vue from 'vue';
import jsonPosts from "../../json/Blog_Posts.json"

export default Vue.extend({
  name: 'DataGrid',

  data: () => ({
    posts: jsonPosts,
    
    props: ['user']
  }),
});
</script>

<style lang="scss">
  ul{
    list-style-type: none
  }
  ul li {
    display: block;
    font-size: 1.7rem;
    font-weight: 500
  }

  ul li span {
    font-weight: 800;
    color: green;

  }
</style> 