<template>
      <div v-if="type === 'login'" class="box">
        <form @submit="authUser" class="form">
          <h2>Войти</h2>
          <div class="inputBox">
            <input
            type="email"
            name="email"
            v-model="authEmail"
            />
            <span>Email</span>
            <i></i>
          </div>
          <div class="inputBox">
            <input
            type="password"
            name="password"
            v-model="authPwd"
            />
            <span>Password</span>
            <i></i>
          </div>
          <div class="links">
            <router-link to="/change-pwd">Сменить пароль</router-link>
            <router-link to="/signup">Зарегистрироваться</router-link>
          </div>
          <input type="submit" value="Войти" class="inp-auth">
        </form>  
      </div>
      <div v-else-if="type === 'signup'" class="box-reg">
        <form @submit="regUser" class="form">
          <h2>Зарегистрироваться</h2>
          <div class="inputBox">
            <input
              type="text"
              name="name"
              v-model="regName"
            />
            <span>Ur name</span>
            <i></i>
          </div>
          <div class="inputBox">
            <input
            type="email"
            required
            name="email"
            v-model="regEmail"
            />
            <span>Ur email</span>
            <i></i>
          </div>
          <div class="inputBox">
            <input
            type="password"
            required
            name="password"
            v-model="regPwd"
            />
            <span>Ur password</span>
            <i></i>
          </div>
          <div class="inputBox">
            <input
            type="password"
            required
            v-model="repeatPwd"
            :class="repeatPwd !== '' && !checkPwd ? 'wrong' : 'success'"
            @input="check"
            />
            <span>Repeat password</span>
            <i></i>
          </div>
          <div class="links">
            <router-link to="/auth">Войти</router-link>
          </div>
          <input type="submit" value="Зарегистрироваться" class="inp-reg">
        </form>
      </div>
      <div v-else>
        <h3>Восстановить пароль</h3>
        ...
        <hr />
        <router-link to="/auth">На страницу входа</router-link>
      </div>
  </template>
  
  <script>
  export default {
    name: "auth-block",
    props: ["type"],
    data() {
      return {
        regName: "",
        regPwd: "",
        repeatPwd: "",
        regEmail: "",
        checkPwd: false,
        authEmail: "",
        authPwd: "",
      };
    },
    methods: {
      regUser: async function (evt) {
        evt.preventDefault();
        this.$router.replace("/profile")
        console.log(this.checkPwd);
        let body = {
          name: this.regName,
          email: this.regEmail,
          password: this.regPwd,
        };
        if (this.checkPwd) {
          const data = await fetch(
            "https://dream-design-server.herokuapp.com/api/users/add",
            {
              method: "post",
              headers: {
                "Content-Type": "application/json",
                Accept: "application.json",
              },
              body: JSON.stringify(body),
            }
          ).then((res) => res.json());
          if (data.message === "ok") {
            evt.target.reset();
            localStorage.setItem("user", JSON.stringify(data.data));
            localStorage.setItem("name", JSON.stringify(data.data.name));
            this.$router.replace("profile");
          } else {
            alert(data.message);
          }
          console.log(data);
        } else {
          alert("пароли не совпадают");
        }
      },
      authUser: async function (evt) {
        evt.preventDefault();
        this.$router.replace("/profile")
        let body = {
          email: this.authEmail,
          password: this.authPwd,
        };
  
        const data = await fetch(
          "https://dream-design-server.herokuapp.com/api/users/auth",
          {
            method: "post",
            headers: {
              "Content-Type": "application/json",
              Accept: "application.json",
            },
            body: JSON.stringify(body),
          }
        ).then((res) => res.json());
  
        if (data.message === "ok") {
          evt.target.reset();
          localStorage.setItem("user", JSON.stringify(data.data));
          localStorage.setItem("name", JSON.stringify(data.data.name));
          this.$router.replace("profile");
        } else {
          alert(data.message);
        }
        console.log(data);
      },
      check: function () {
        this.checkPwd = this.regPwd === this.repeatPwd;
      },
    },
  };
  </script>
  
  <style scoped>
  .wrong {
    border-color: orangered;
  }
  .success {
    border-color: mediumseagreen;
  }
  .box {
    position: relative;
    width: 400px;
    height: 420px;
    background: #1c1c1c;
    border-radius: 8px;
    overflow: hidden;
    left: 33%;
  }
  .box::before, .box-reg::before {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 380px;
    height: 420px;
    /* background: linear-gradient(0deg, transparent, transparent, #45f3ff); */
    background: linear-gradient(0deg, transparent, transparent, #0091ff);
    transform-origin: bottom right;
    animation: animate 6s linear infinite;
  }
  @keyframes animate {
    0% {
      transform: rotate(0deg);
    }
    100% {
      transform: rotate(360deg);
    }
  }
  .box::after ,.box-reg::after {
    content: '';
    position: absolute;
    top: -50%;
    left: -50%;
    width: 380px;
    height: 420px;
    /* background: linear-gradient(0deg, transparent, transparent, #45f3ff); */
    background: linear-gradient(0deg, transparent, transparent, #0091ff);
    transform-origin: bottom right;
    animation: animate 6s linear infinite;
    animation-delay: -3s;
  }
  .form {
    position: absolute;
    inset: 2px;
    border-radius: 8px;
    background: #28292d;
    z-index: 10;
    padding: 50px;
    display: flex;
    flex-direction: column;
  }
  .form h2 {
    /* color: #45f3ff; */
    color: #0091ff;
    font-weight: 500;
    text-align: center;
    letter-spacing: 0.1em;
  }
  .inputBox {
    position: relative;
    width: 300px;
    margin-top: 35px;
  }
  .inputBox input {
    position: relative;
    width: 100%;
    padding: 20px 10px 10px;
    background: transparent;
    border: none;
    outline: none;
    color: #23242a;
    font-size: 1em;
    letter-spacing: 0.05em;
    z-index: 10;
  }
  .inputBox span {
    position: absolute;
    left: 0;
    padding: 20px 0 10px;
    font-size: 1em;
    color: #8f8f8f;
    pointer-events: none;
    letter-spacing: 0.05em;
    transition: 0.5s;
  }
  .inputBox input:valid ~ span,
  .inputBox input:focus ~ span {
    /* color: #45f3ff; */
    color: #0091ff;
    transform: translateX(0px) translateY(-34px);
    font-size: 0.75em;
  }
  .inputBox i {
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    height: 2px;
    /* background: #45f3ff; */
    background: #0091ff;
    border-radius: 4px;
    transition: 0.5s;
    pointer-events: none;
    z-index: 9;
  }
  .inputBox input:valid ~ i,
  .inputBox input:focus ~ i {
    height: 44px;
  }
  .links {
    display: flex;
    justify-content: space-between;
  }
  .links a {
    margin: 10px 0;
    font-size: 0.75em;
    color: #8f8f8f;
  }
  .links a:hover,
  .links a:nth-child(2) {
    /* color: #45f3ff; */
    color: #0091ff;
  }
  .inp-auth[type="submit"] {
    border: none;
    outline: none;
    /* background: #45f3ff; */
    background: #0091ff;
    padding: 11px 25px;
    width: 100px;
    margin-top: 10px;
    border-radius: 4px;
    font-weight: 600;
    cursor: pointer;
  }
  input[type="submit"]:active {
    opacity: 0.8;
  }
  .box-reg {
    position: relative;
    width: 400px;
    height: 545px;
    background: #1c1c1c;
    border-radius: 8px;
    overflow: hidden;
    left: 33%;
  }
  .inp-reg {
    border: none;
    outline: none;
    /* background: #45f3ff; */
    background: #0091ff;
    padding: 11px 25px;
    width: 185px;
    margin-top: 10px;
    border-radius: 4px;
    font-weight: 600;
    cursor: pointer;
}
  </style>