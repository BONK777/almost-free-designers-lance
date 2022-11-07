<template lang="">
  <div class="container">
  <div class="page">
    <div class="left">
      <h1>Найди самого лучшего дизайнера</h1>
      <p>Apple's remarkable new personal computer</p>
      <router-link class="btn" to="/auth">Искать!</router-link>
      <!-- <button>find</button> -->
      
    </div>
    <div class="right">
      <div class="img"><img src="https://external-content.duckduckgo.com/iu/?u=https%3A%2F%2Fsebastien-compagne.fr%2Fwebsite%2Fzpg%2Farcheologeek%2F1990_-_apple_mac_classic_II.png&f=1&nofb=1">
      </div>
      <ul>
        <li>Instagram</li>
        <li>-</li>
        <li>Facebook</li>
        <li>-</li>
        <li>Twitter</li>
      </ul>
    </div>
  </div>
</div>
  </template>
  
  <script>
  
  export default {
    name: "home-page"
    };
  </script>
  <style scoped>
@import url('https://fonts.googleapis.com/css2?family=Red+Hat+Mono&display=swap');

*{
  margin: 0;
  padding:0;
}

body{
  background-color: #4044ab;
}

.page {
  height: 79%;
  width: 90%;
  position: absolute;
  background-color: #282944;
  top:50%;
  left:50%;
  transform: translate(-50%,-50%);
}

a {
  text-decoration:none;
  color: #534935;
  text-transform:uppercase;
  font-size: 12px;
  font-family: 'Red Hat Mono', monospace;
}

a img {
  height:2.3rem;
  margin: 10px 0 0 50px;
}

.navbar {
  width: 100%;
  height:10%;
  position: sticky;
  background-color:white;
}

.navbar ul{
  display: flex;
  float: right;
  list-style-type:none;
  text-decoration: none;
  margin:15px 15px;
}

.navbar ul li{
  padding: 0 15px 0 15px;
}

.right{
  /* background-color: #45f3ff; */
  background-color: #0091ff;
  position: absolute;
  width:55%;
  height: 100%;
  left: 45%;
  border-radius: 100% 0 0 0;
}

h1 {
  font-family: 'Red Hat Mono', monospace;
  color: ghostwhite;
  position: absolute;
  top: 40%;
  left: 8%;
  transform: translate(-10%, -40%);
  width: 350px;
  font-size:2.3rem;
}

p{
  font-family: 'Red Hat Mono', monospace;
  color: ghostwhite;
  position: absolute;
  top: 58%;
  left: 7%;
  transform: translate(-7%, -58%);
 font-size: 12px;
}

.btn{
  position: absolute;
  top:65%;
  left:6%;
  transform: translate(-5%, -65%);
  border-radius: 15px;
  background-color: #0091ff;
  width:125px;
  height: 35px;
  color: ghostwhite;
  border-style: none;
  display: flex;
  justify-content: center;
  align-items: center;
  letter-spacing: 1px;
  font-weight: 600;
  transition: 0.5s;
}

.btn:hover{
  box-shadow: 0 5px 15px #0091ff;
  cursor: pointer;
}

.right img{
  position: absolute;
  top:15%;
  left: 5%;
  height:20rem;
  transform: translate(-5%, -5%);
transform:rotate(-20deg);
  
}

.right ul {
  display: flex;
  float: right;
  list-style-type:none;
  text-decoration: none;
  margin:15px 15px;
  top:50%;
  left: 60%;
  position:absolute;
  transform:rotate(-90deg);
}

.right ul li{
  margin: 8px;
  color:#534935;
  font-family: 'Red Hat Mono', monospace;
  transform:uppercase;
  font-size: 10px;
}
</style>