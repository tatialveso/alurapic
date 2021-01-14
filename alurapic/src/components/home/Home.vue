<template>
  <div>
    <h1 class="title">{{ titulo }}</h1>
    <input type="search" class="filtro" @input="filtro = $event.target.value" placeholder="filtre pelo título da foto">
    {{ filtro }}
    <ul class="photoList">
      <li class="photoListItem" v-for="foto of fotosComFiltro">
        <painel :titulo="foto.titulo">
          <imgResp :url="foto.url" :titulo="foto.titulo" />
          <meu-botao rotulo="remover" tipo="button" @botaoAtivado="remove(foto)" :confirmacao="false"  estilo="padrao"/>
        </painel>
      </li>
    </ul>
  </div>
</template>

<script>
  import Painel from '../shared/painel/Painel.vue';
  import ImgResp from '../shared/img-resp/ImgResp.vue';
  import Botao from '../shared/botao/Botao.vue';

  export default {
    components:  {
      'painel': Painel,
      'imgResp': ImgResp,
      'meu-botao': Botao
    },

    methods: {
      remove(foto) {
        if(confirm('Confirma?')) {
          alert(foto.titulo);
        }
      }
    },

    data() {
      return {
        titulo: 'Alurapic',
        fotos: [],
        filtro: ''
      }
    },

    computed: {
      fotosComFiltro() {
        if(this.filtro) {
          let exp = new RegExp(this.filtro.trim(), 'i');
          return this.fotos.filter(foto => exp.test(foto.titulo));
        } else {
          return this.fotos;
        }
      }
    },

    created() {
      this.$http.get('http://localhost:3000/v1/fotos')
        .then(res => res.json())
          .then(fotos => this.fotos = fotos, error => console.log(err));
    }
  }
</script>

<style>
  .title {
    text-align: center;
  }

  .filtro {
    display: block;
    width: 100%;
  }

  .photoList {
    list-style: none;
  }

  .photoListItem {
    display: inline-block;
  }
</style>
