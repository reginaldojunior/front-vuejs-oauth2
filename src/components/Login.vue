<template>
  <div class="ui grid">
    <div class="eight wide column landing-image"></div>
    <div class="four wide column box-center">
      <h1>Faça o Login</h1>

      <form v-on:submit="handleSubmit($event)">
        <div class="ui form segment">
          <div class="field">
            <label>E-mail</label>
            <div class="ui left labeled icon input">
              <input type="text" placeholder="Digite seu e-mail" v-model="user.email">
            </div>
          </div>
          <div class="field">
            <label>Senha</label>
            <div class="ui left labeled icon input">
              <input type="password" placeholder="Digite sua Senha" v-model="user.password">
            </div>
          </div>
          <div class="ui error message">
            <div class="header">We noticed some issues</div>
          </div>
          <button class="ui blue submit button">Login</button>
        </div>
      </form>

    </div>
  </div>
</template>

<script>
export default {
  name: 'login',
  data () {
    return {
      user: {
        email: null,
        password: null
      }
    }
  },
  methods: {
    handleSubmit: function (e) {
      e.preventDefault()

      this.$auth.login({
        params: this.user,
        method: 'POST',
        success: function (data) {
          localStorage.token = data['body']['token']
        },
        rememberMe: true,
        redirect: '/dashboard'
      })
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  
.landing-image {
  background-image: url('https://images.pexels.com/photos/315582/pexels-photo-315582.jpeg?w=940&h=650&auto=compress&cs=tinysrgb') !important;
  background-size: cover !important;
  height: 700px;
}

.box-center {
  margin-left: 13%;
  margin-top: 10%;
}

</style>
