<template>
  <div v-if="!loggin" class="container">
      <div class="row mt-5 justify-content-center">
        <div class="col-md-3">
          <div class="card shadow-lg">
            <div class="card-header bg-success text-white">
              <p class="h3">Ingreso</p>
            </div>
            <div class="card-body bg-light">
              <form @submit.prevent="valida()">
                <div class="mb-2">
                  <input v-model="user.email"  class="form-control" placeholder="Email" type="email">
                </div>
                <div class="mb-2">
                  <input v-model="user.password"  class="form-control" placeholder="Password" type="password">
                </div>
                <div class="mb-2">
                  <input class="btn btn-success" type="submit" value="Ingresar">
                </div>
              </form>
            </div>
          </div>
        </div>
      </div>
    </div>
    <div v-if="loggin" class="container">
      <router-view />
    </div>
</template>

<script>
import { UserService } from "@/services/UserService";

export default {
  name: 'App',
  data: function() {
      return {
        usuarios: [],
        loggin: false,
        user: {
            email: '',
            password: ''
        }
    };
  },
  created: async function() {
    try {
      let response = await UserService.getAllUsers();
      this.usuarios = response;
    } catch (error) {
      this.errorMessage = error;
    }
  },
  methods: {
    valida: function() {
        let encontro = this.usuarios.map(element=> element.email).indexOf(this.user.email)
        console.log(encontro)
        if (encontro !== -1) {
            if (this.user.password === this.usuarios[encontro].password) {
                this.loggin = true
            }else{
                this.loggin = false
            }
        }else{
            this.loggin = false
        }
        if (this.loggin) {
            console.log('Usuario Logueado')
            this.$router.push('/home')
        }else{
            console.log('Usuario NO Logueado')
        }
    }
  }
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
