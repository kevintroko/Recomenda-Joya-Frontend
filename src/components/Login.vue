<template>
  <b-container>
    <b-form>
      <b-form-group label = "Login">
          <b-form-input
            placeholder="Usuario"
            v-model.trim="username"
            required>
          </b-form-input>
          <b-form-input
            placeholder="Contraseña"
            v-model.trim="password"
            required>
          </b-form-input>
      </b-form-group>
      <b-button type="login" variant="primary" @click="login">Login</b-button>
    </b-form> 
  </b-container>
</template>

<script>
import Vue from 'vue'

export default {
  name: 'Login',
  data(){
    return{
      username: "",
      password: "",
    }
  },
  methods: {
    login() {
      // Puro humo
      if (!this.validate(this.username, this.password)) return;
      this.logged(this.username);
    },
    // OIIII nomas!
    validate(username, password) {
      return username == password;
    },
    logged(id) {
      Vue.prototype.$userId = id;
      this.$router.push({ name: 'home' });
    },
  }
}

</script>
