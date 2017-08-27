<template>
  <div class="ui message">
    <div class="header">
      Dados Pessoais
    </div>
    <p>
      Nome: {{user.name}} </br>
      Email: {{user.email}} </br>
    </p>
  </div>
</template>

<script>
export default {
  name: 'dashboard',
  data () {
    return {
      user: {
        name: null,
        email: null
      }
    }
  },
  created () {
    this.getData()
  },
  methods: {
    getData () {
      this.$http.post(process.env.API + '/api/details', function (data) {
      }, {headers: {'Authorization': 'Bearer ' + localStorage.token}})
      .then(response => {
        this.user.name = response['body']['user']['name']
        this.user.email = response['body']['user']['email']
      })
    }
  }
}
</script>