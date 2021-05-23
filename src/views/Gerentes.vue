<template>
  <div class="container">
    <h1>Gerentes</h1>
    <div class="row">
      <Gerente v-for="gerente in gerentes" :key="gerente.numero" :gerente="gerente" />
    </div>
  </div>
</template>

<script>
import Gerente from '@/components/Gerente.vue'

export default {
  components: {
    Gerente
  },
  data() {
    return {
      gerentes: []
    }
  },
  //renderizado tdas as vezes que o componente é executado na tela
  mounted(){
    this.$http.get('gerentes')
      .then(res => this.gerentes = res.data)
      .catch(err => console.log(err))
  },
  //antes do componente renderizar
  beforeRouterEnter(to, from, next){
    if(!this.$store.state.token){
      console.log('Não pode acessar deslogado!!!');
      next({name: 'login'})
    }
    next()
  }
}
</script>

<style>

</style>