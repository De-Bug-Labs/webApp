<template>
  <div class="nav" v-if="regular">
    <router-link to="/" class="logo1"
      ><img src="../public/img/logo1.png" />
    </router-link>
    <a class="toggle" @click="mobile = !mobile"
      ><i class="large material-icons">dehaze</i></a
    >
    <ul :class="{ active1: mobile }" @click="mobile = !mobile">
      <li>
        <router-link to="/somos"
          >Somos <img src="../public/img/teamwork.png"
        /></router-link>
      </li>
      <li>
        <router-link to="/about"
          >Nosotros <img src="../public/img/g.svg"
        /></router-link>
      </li>
      <li>
        <router-link to="/material"
          >Material <img src="../public/img/globe.svg"
        /></router-link>
      </li>
      <li>
        <router-link to="/help"
          >Ayuda <img src="../public/img/information.svg"
        /></router-link>
      </li>
      <li v-if="view.status">
        <router-link to="/donaciones"
          >Apóyanos <img src="../public/img/love.svg"
        /></router-link>
      </li>
      <li>
        <router-link to="/calendar"
          >Calendario <img src="../public/img/calendar.svg"
        /></router-link>
      </li>
      <li>
        <router-link to="/salon"
          >Salón de la fama <img src="../public/img/trophy.svg"
        /></router-link>
      </li>
    </ul>
  </div>
  <router-view
    @admin="regular = false"
    @click="mobile = false"
    @volver="regular = true"
  />
</template>

<script lang="ts">
import { defineComponent } from "vue";
export default defineComponent({
  data() {
    return {
      mobile: false,
      regular: true,
      view: { id: "", status: false, name: "" },
      completeQuery: false,
    };
  },
  methods: {
    getInfo() {
      this.completeQuery = false;
      try {
        const data = fetch("/api/view", { credentials: "include" })
          .then((res) => res.json())
          .then((data) => {
            this.view = data;
          });
      } catch (error) {
        console.log(error);
      }
      this.completeQuery = true;
    },
  },
  mounted() {
    this.getInfo();
  },
});
</script>

<style lang="scss">
@import url("https://fonts.googleapis.com/css2?family=Signika:ital,wght@0,200;0,300;0,400;0,600;0,700;1,200;1,300;1,400;1,600&display=swap");
@import url("https://fonts.googleapis.com/icon?family=Material+Icons");
@import url("https://fonts.googleapis.com/css2?family=Open+Sans:ital,wght@0,200;0,300;0,400;0,600;0,700;1,200;1,300;1,400;1,600&display=swap");

body::-webkit-scrollbar {
  display: none;
}
body {
  margin: 0;
  overflow-x: hidden;
  min-height: 100%;
  display: flex;
  flex-direction: column;
  line-height: 1.6;
}
#app {
  margin-top: 100px;
}

.nav {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100px;
  padding: 10px 40px;
  box-sizing: border-box;
  transition: 0.5s;
  background-color: #8edafd;
  box-shadow: 0px 3px 5px rgba(0, 0, 0, 0.2);
  z-index: +1;

  .logo1 {
    float: left;
    text-decoration: none;
    font-family: "Signika", sans-serif;
    display: flex;
    flex-direction: row;
    text-align: center;
    height: 70px;
    transition: 0.5s;

    p {
      margin-left: 5px;
      margin-bottom: 0px;
      margin-top: 10px;
      color: #000;
      font-size: 3rem;
      font-weight: 600;
      position: relative;
    }

    img {
      height: 80px;
      width: 200px;
      transition: 0.5s;
    }
  }

  ul {
    position: relative;
    float: right;
    margin: 0;
    padding: 0;
    display: flex;

    li {
      list-style: none;
      a {
        position: relative;
        padding: 5px 15px;
        margin: 20px 0;
        color: black;
        text-decoration: none;
        font-size: 15px;
        font-family: "Open Sans", sans-serif;
        font-weight: 700 !important;
        display: flex;

        img {
          height: 25px;
          transition: 0.5s;
          margin-left: 10px;
        }
        &:hover {
          border-bottom: 2px solid rgb(0, 0, 0);
        }
        &.router-link-exact-active {
          border-bottom: 2px solid rgb(0, 0, 0);
        }
      }
    }
  }
}

.toggle {
  display: none;
  position: absolute;
  right: 10px;
  top: 26px;
  color: rgb(0, 0, 0);
  padding: 5px;
  cursor: pointer;
  font-size: 24px;
}

@media screen and (max-width: 1320px) {
  .nav {
    padding: 0 0;
    width: 100vw;
    ul {
      li {
        a {
          display: flex;
          padding: 10px 10px;
          font-size: 15px;
          img {
            height: 20px;
            margin-left: 5px;
          }
        }
      }
    }
    .logo1 {
      margin-top: 10px;
      margin-left: 10px;
    }
  }
}

@media screen and (max-width: 1030px) {
  .footer {
    h1 {
      margin-left: 20px;
      font-size: 15px;
    }
  }
  .nav {
    padding: 0 0;
    width: 100vw;

    ul {
      width: 100%;
      top: 16px;
      display: none;
      border-top: 3px solid rgb(0, 0, 0);

      li {
        border-bottom: 3px solid rgb(0, 0, 0);
        text-align: center;
        a {
          margin: 0;
          display: flex;
          color: rgb(0, 0, 0);
          background: #8edafd;
          text-transform: uppercase;
          align-items: center;

          img {
            padding-top: 5px;
          }

          &.router-link-exact-active {
            background: #ffffff;
            border-bottom: none;
          }
          &:hover {
            background: #ffffff;
            border-bottom: none;
          }
        }
      }
    }

    ul.active1 {
      display: block;
    }

    .logo1 {
      margin-top: 10px;
      margin-left: 10px;
    }
    .toggle {
      right: 10px !important;
      display: block !important;
      i {
        font-size: 30px;
      }
    }
  }
}
</style>
