<template>
  <div class="modal">
      <div class="modal-close" @click="$emit('modalClose')">+</div>
      <h1>Add project!</h1>
      <small>You will be contacted as soon as possible</small>
      <form @submit.prevent="addProject">
          <input type="text" v-model="title" placeholder="Название проекта" required>
          <input type="text" v-model="image" placeholder="Фото проекта">
          <input type="text" v-model="link" placeholder="Ссылка на продукт">
          <input type="month" v-model="date" placeholder="Когда велась работа над проектом?" >
          <textarea v-model="text" placeholder="Описание"></textarea>
          <button type="submit" class="formBtn">Добавить</button>
      </form>
  </div>
</template>

<script>
export default {
  name: "modal-form",
  data() {
      return {
          title: "",
          image: "",
          text: "",
          link: "",
          date: null,
          tags: []
      }
  },
  methods: {
      addProject() {
          let user = localStorage.getItem("user");
          if (user) {
              user = JSON.parse(user);
          }
          const body = {
              title: this.title,
              link: this.link,
              main_image: this.image,
              description: this.text,
              tags: this.tags,
              date: this.date && new Date(this.date)
          }
          // console.log(body);
          // console.log(user);
          if (user) {
              fetch(`https://dream-design-server.herokuapp.com/api/users/project/add/${user._id}`, {
                  method: "PATCH",
                  headers: {
                      "Content-Type": "application/json",
                      "Accept": "application/json"
                  },
                  body: JSON.stringify(body)
              })
              .then(res => res.json())
              .then(data => {
                  // console.log(data);
                  if (data.message === "ok") {
                      this.clearForm();
                      user = data.data;
                      localStorage.setItem("user", JSON.stringify(user));
                      this.$emit("modalClose");
                      this.$emit("updateData", user);
                  }
              })
          }
      },
      clearForm() {
          this.title = "";
          this.link = "";
          this.image = "";
          this.text = "";
          this.tags = [];
          this.date = null;
      }
  }
}
</script>

<style scoped>
  .modal form {
    display: flex;
    flex-direction: column;
  }
  h1 {
    font-size: 2.2rem;
  }
  small {
    color: #666;
    font-size: 12px;
  }
  .formBtn {
    width: 140px;
    display: inline-block;
    background: #0091ff;
    border-radius: 5px;
    color: #fff;
    font-weight: 100;
    font-size: 1.2em;
    border: none;
    height: 30px;
  }
  input, textarea { 
  margin: .8em auto;
  font-family: inherit; 
  text-transform: inherit; 
  font-size: inherit;
  
  display: block; 
  width: 280px; 
  padding: .4em;
}
textarea { height: 80px; resize: none; }
/* * { box-sizing: border-box; }
h1{margin: 0;}
.modal { 
  display: flex;
  border: 6px solid salmon; 
  padding: 2em;
  width: 400px;
  text-align: center;
  background: #fff;
  position: fixed;
  top:50%;
  left:50%;
  transform: translate(-50%,-50%);
  -webkit-transform: translate(-50%,-50%)
  
}

input, textarea { 
  margin: .8em auto;
  font-family: inherit; 
  text-transform: inherit; 
  font-size: inherit;
  display: block; 
  width: 280px; 
  padding: .4em;
}
textarea { height: 80px; resize: none; }

.formBtn { 
  width: 140px;
  display: inline-block;
  
  background: teal;
  color: #fff;
  font-weight: 100;
  font-size: 1.2em;
  border: none;
  height: 30px;
} */
</style>