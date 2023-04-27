<template>
  
  <nav class="main-nav">
    
    <a class="navbar-header" href="https://www.instagram.com/wensmens/"><img src="../../data/img/wensmens_logo.png" ondragstart="return false;" alt="logo"/></a>
    <router-link :to="{ name: 'Home' }">Wensen</router-link>
    <router-link :to="{ name: 'AddProject' }">Doe een wens!</router-link>
  </nav>
  
</template>

<script>
export default {

}
</script>
<style>
  .navbar-header img{
    
    height: 120px;
    position: relative;
    top: 45px;
    align-items: flex-start;
    
  }
  .main-nav {
    text-align: center;
    align-items: center;
    align-content: center;
    margin: 40px auto;
    height: 120px;
    
  }
  .main-nav a{  
    display: inline-block;
    text-decoration: none;
    margin: 0 10px;
    color: rgb(190, 68, 68);
    font-size: 30px;
    
  }
  a.router-link-active {
    border-bottom: 3px solid #00ce89;
    padding-bottom: 4px;
    border-radius: 3px;
  }
</style>