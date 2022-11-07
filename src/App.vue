<!--
    TODO: Мы хотим создать сервис по поиску графических дизайнеров / художников
    Что должен делать сервис?
        Дизайнер регистрируется на сайте и заполняет свой профиль. - Что должно быть в профиле? (Портфолио)
            - кто я
            - мои работы (картинки / описание)
            - моя автобиография
            - мои навыки
        Пользователь хочет найти дизайнера - ищет по фильтрам, выбирает страницу дизайнера, смотрит портфолио, пишет в чат дизайнеру

    Надо:
        Найти похожие сайты оказания фриланс-услуг (по специализации художника)
        Найти положительные и отрицательные моменты во всех подобных сайтах
        Список этих моментов выложить в канале группы:
            Картинка (скриншот) + комментарий
        Можно искать как по реальным сайтам, так и по сервисам с дизайном

-->

<template>
      <!-- <button v-on:click="modalOpen">click</button> -->
      <main-container @showPopup="modalOpen" :userData="userData"></main-container>
      <div class="modal-wrapper" :style="{display: modalActivity ? 'flex' : 'none'}">
        <add-project @modalClose="modalClose"  @updateData="updateUserData"/>
      </div>
</template>
  
  <script>
  import MainContainer from "@/components/Main/index.vue";
  import AddProject from "@/components/addProject/index.vue";
  
  export default {
    name: "App",
    components: {
      MainContainer,
      AddProject
    },
    data() {
      return {
          modalActivity: false,
          userData: {},
      }
    },
    methods: {
        modalOpen() {
            this.modalActivity = true;
        },
        modalClose() {
            this.modalActivity = false;
        }
    },
    created() {
      let user = localStorage.getItem("user");
      if(user){
        this.userData = JSON.parse(user);
      }
    },
  };
  </script>
    
  <style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    text-decoration: none;
    font-family: monospace, sans-serif;
    /* color: ghostwhite; */
  }
  body {
    display: flex;
    justify-content: center;
    align-items: center;
    min-height: 100vh;
    background: #23242a;
  }
  .modal-wrapper {
        position: fixed;
        display: flex;
        top: 0;
        left: 0;
        right: 0;
        bottom: 0;
        align-items: center;
        justify-content: center;
        background-color: #0004;
        /*backdrop-filter: blur(1px);*/
    }
    .modal {
        background-color: #fff;
        padding: 70px;
        border-radius: 8px;
        position: relative;
    }
    .modal-close {
        position: absolute;
        top: 6px;
        right: 10px;
        line-height: 1;
        transform: rotate(45deg);
        cursor: pointer;
    }
  </style>