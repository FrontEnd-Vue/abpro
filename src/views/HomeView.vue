<template>
  <NavBar />
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Bienvenidos"/>
  </div>
</template>

<script>
import HelloWorld from '@/components/HelloWorld.vue'
import NavBar from "@/components/NavBar";
export default {
  name: 'HomeView',
  components: {
    NavBar,
    HelloWorld
  }
}
</script>
