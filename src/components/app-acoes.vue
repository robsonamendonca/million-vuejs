<template>
<main class="bd-masthead" id="content" role="main">
  <div class="container">
    <div class="row">
      <div class="col-6 mx-auto col-md-4 order-md-2">
        
           <img :src="require('../assets/logo.png')" width="512" height="430"  />        

      </div>
      <div class="col-md-8 order-md-1 text-center text-md-left pr-md-5">
        <h1 class="mb-3">Ações</h1>
            <router-link to="/acoes/novo" tag="button" class="btn btn-lg btn-bd-primary mb-3 mr-md-3" >Novo</router-link>
      <section v-if="errored">
        <p>Pedimos desculpas, não estamos conseguindo recuperar as informações no momento. Por favor, tente novamente mais tarde.</p>
      </section>

        <div v-if="loading">
          <div class="d-flex justify-content-center">
            <div class="spinner-border" role="status">
              <span class="sr-only">Loading...</span>
            </div>
          </div>
         </div>            
        <div v-else>
        <table class="table table-bordered table-sm">
            <thead>
              <tr>
                <th>ID</th>
                <th>Nome</th>
                <th>Preço</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="acao in acoes" v-bind:key="acao.id"> 
                <td>{{acao.id}}</td>
                <td>{{acao.nome}}</td>
                <td>R$ {{acao.preco}}</td>
              </tr>
            </tbody>
          </table>     
        </div> 
      </div>
    </div>
    
  </div>
</main> 
</template>

<script>
import axios from 'axios';
export default {
  name: "Acoes",
  data: () => {
    return {
      robson: "Mandou muito bem",
      acoes: [],
      loading: true,
      errored: false          
    }
  },
  methods: {
    lista(){
      axios.create({
        baseURL: 'https://acoes-service-prod.herokuapp.com/acoes.json',
        headers: {'token': '123456'}
      }).get().then((res) => {
        console.log(res.data)
        this.acoes = res.data
      })
      //axios.get(`https://acoes-service-prod.herokuapp.com/acoes.json`)
      .catch(error => {
              console.log(error)
              this.errored = true
            })
            .finally(() => this.loading = false)          
    }
  },
  created(){
    this.lista();
  }
}
</script>
