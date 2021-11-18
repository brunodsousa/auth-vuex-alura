<template>
  <div class="container">
    <h1>Login</h1>
    <form @submit.prevent="efetuarLogin">
      <div class="form-group">
        <label for="email">E-mail</label>
        <input
          type="email"
          id="email"
          class="form-control"
          v-model="usuario.email"
        />
      </div>
      <div class="form-group">
        <label for="senha">Senha</label>
        <input
          type="password"
          id="senha"
          class="form-control"
          v-model="usuario.senha"
        />
      </div>
      <p class="alert alert-danger" v-if="errorMessage">{{ errorMessage }}</p>
      <button type="submit" class="btn btn-primary btn-block">Logar</button>
      <router-link :to="{ name: 'novo.usuario' }">
        Não possui um cadastro? Cadastre-se aqui!
      </router-link>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      usuario: {
        email: "",
        password: "",
      },
      errorMessage: "",
    };
  },
  methods: {
    efetuarLogin() {
      // this.$http
      //   .post("auth/login", this.usuario)
      //   .then((response) => {
      //     console.log(response);
      //     // localStorage.setItem("token", response.data.access_token);
      //     // this.$store.state.token = response.data.access_token;
      //     // this.$store.state.usuario = response.data.user;
      //     this.$store.commit("DEFINIR_USUARIO_LOGADO", {
      //       token: response.data.access_token,
      //       usuario: response.data.user,
      //     });
      //     this.$router.push({ name: "gerentes" });
      //   })
      //   .catch((error) => console.log(error));

      this.$store
        .dispatch("efetuarLogin", this.usuario)
        .then(() => {
          this.$router.push({ name: "gerentes" });
          this.errorMessage = "";
        })
        .catch((error) => {
          if (error.request.status === 401) {
            this.errorMessage = "E-mail ou senha inválidos.";
          }
        });
    },
  },
};
</script>

<style scoped>
</style>