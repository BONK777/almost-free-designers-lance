<template>
    <div>
      <h1>test is here</h1>
      <div class="container">
        <div class="card" v-for="u of users" :key="u.email">
          <router-link class="name" :to="{ name: 'userProfile', params: { id: u._id } }">{{ u.name || "NoName" }}</router-link>
          <hr />
          <p class="email">{{ u.email }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  // TODO: Используя localStorage, переписать шапку так, чтобы при наличии пользователя не было кнопок входа, а при отсутствии пользователя не было ссылки на личный кабинет.
  // TODO: На странице пользователя (можно в шапке), добавить кнопку "выйти" - очистить localStorage.
  // TODO: Отображать в личном кабинете данные авторизованного пользователя
  
  export default {
      data() {
          return {
              users: []
          }
      },
     name: "test-data",
     created() {
      fetch("https://dream-design-server.herokuapp.com/api/users")
          .then(res => res.json())
          .then(data => {
              if (data.message === "ok") {
                  this.users = data.data;
              }
          })
     }
  };
  </script>

  <style scoped>
  * {
    color: ghostwhite;
    margin: 5px;
  }
  hr {
    background: linear-gradient(225deg,ghostwhite, #0091ff);
    border: none;
    height: 1px;
  }
  .name {
    transition: 0.5s;
  }
  .name:hover {
    color: #0091ff;
  }
  .email {
    color: royalblue;
  }
</style>