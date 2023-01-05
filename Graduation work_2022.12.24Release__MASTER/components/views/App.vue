<template>
<header class="header">
  <fa class="fa-bars" :icon="['fas','bars']" @click="toggleSideNav" />
  <fa  @click="logout" class="fa-sign-out" :icon="['fas','arrow-right-from-bracket']"></fa>
</header>


<!-- <main>

    <router-view/>
</main> -->

</template>



<script>
import { getAuth, onAuthStateChanged } from "firebase/auth";
import 'normalize.css'
import SideNav from "./components/SideNav.vue"
// storeのjsのActionsを呼び出している
import { mapActions } from "vuex"

export default {
  name: 'App' ,
  components: {
    SideNav
  },
methods: {
  ...mapActions([ "toggleSideNav" ,"setLoginUser","logout","deleteLogin","fetchTasks"])
},
created(){
  const auth = getAuth();
  onAuthStateChanged(auth, (user) => {
  if (user) {
    this.setLoginUser(user)
    this.fetchTasks()
  } else {
    this.deleteLoginUser()
  }
  
});
}



<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  // text-align: center;
  // color: #2c3e50;
}


  


*{
  box-sizing: border-box;
}


h1,h2,p{
  margin: 0;
}

body{
  background-color: #8a47cc;
}

.header{
  background-color: #562d80;
  height: 56px;
  width: 100%;
  display:flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 20px;
  box-shadow: 0 3px 6px rgba($color: #000000, $alpha: 0.16);
  position: fixed;
  // 重なり順番を調整
  z-index: 1;
}

.fa-bars,.fa-sign-out{
  color:#fff;
  font-size:20px;
}


nav {
  padding: 30px;

  a {
    font-weight: bold;
    color: #2c3e50;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>

 

}

</script>