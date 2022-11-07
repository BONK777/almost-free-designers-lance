<template>
    <header class="header">
      <nav>
        <router-link to="/"> Home </router-link>
        <router-link v-if="user" to="/profile"> Profile </router-link>
        <router-link v-if="user" to="/test"> Our Designers! </router-link>
        <router-link v-if="!user" to="/auth"> Auth </router-link>
        <button v-if="user" @click="logout" class="logout">Log Out</button>
      </nav>
    </header>
  </template>
  
  <script>
  export default {
    name: "usr-header",
    data() {
      return {
        isPopup: false,
        user: localStorage.getItem("user")
      };
    },
    methods: {
    //   setIsPopup() {
    //     this.isPopup = !this.isPopup;
    //   },
      logout() {
        localStorage.removeItem("user");
        localStorage.removeItem("name");
        this.$router.replace("/")
      }
    },
  };
  </script>
  
  <style scoped>
  a {
    color: ghostwhite;
    margin: 5px;
    font-size: 20px;
    position: relative;
  }
  a:after {
    content: "";
    position: absolute;
    background-color: #0091ff;
    height: 3px;
    width: 0;
    left: 0;
    bottom: -10px;
    transition: 0.3s;
  }
  a:hover::after {
    width: 100%;
  }
  .header {
    width: 1200px;
    margin: 0 auto;
    /* display: flex;
    justify-content: center;
    align-items: center; */
    padding: 20px 0;
    background: #23242a;
  }
  nav {
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .logout {
    background-color: #0091ff;
    width:125px;
    height: 35px;
    color: ghostwhite;
    border-style: none;
    border-radius: 15px;
    cursor: pointer;
    transition: 0.5s;
  }
  .logout:hover{
  box-shadow: 0 5px 15px #0091ff;
  cursor: pointer;
}
  </style>