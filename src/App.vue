<template>
  <div class="main-item">
    <router-view /> 
  </div>
</template>


<script lang="ts">
import Vue from 'vue';

export default Vue.extend({
  name: 'App',

})
</script>

<style lang="scss">
   @import "~bootstrap/dist/css/bootstrap.css";

  input:focus, input:active{
    box-shadow: none !important;
    outline: 0 !important;
    text-shadow: none;
  }

</style> 