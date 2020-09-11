<template>
  <div id="app">

    <h1 :title="dica" v-if="isShow"> {{tituloAula}} - v-if</h1>
    <h1 :title="dica" v-show="isShow"> {{tituloAula}} - v-show</h1>
    <p> {{data}} </p>

    <p> {{aluno.nome}} </p>
    <p> {{aluno.media + 1}} </p>

    <lista-carros :carros="carros"></lista-carros>

    <hr/>

    <form-carro @adicionar="adicionarCarro2"></form-carro>

    <hr/>

    <input type="text" v-model="filtro" placeholder="Filtrar pelo nome"/>
    <table>
      <tr>
        <th>Nome</th>
        <th>Preço</th>
      </tr>
      <tr v-for="c in carrosFiltrados" :key="c.nome">
        <td> {{c.nome}} </td>
        <td> {{c.preco}} </td>
      </tr>
    </table>

    <p :class="{'totalMaior10k': total > 10000, 'totalMaior20k': total > 20000}">{{total}}</p>

    


    <button @click="updateDate()">Update date</button>
    <button @click="isShow = !isShow">Mostrar/Esconder título</button>

    <button @click="adicionarCarro()">Adicionar carro</button>
    <button @click="adicionarCarro2()">Adicionar carro 2</button>
    
  </div>
</template>

<script>


// JSON - Javascript Object Notation
import ListaCarros from './components/ListaCarros'
import FormCarro from './components/FormCarro'
// import '@/components/ListaCarros'
export default {
  components: {
    ListaCarros, FormCarro
  },

  data() {
    return {
      tituloAula: 'Aula 01 VueJS',
      data: new Date(),
      dica: 'Este é um título',
      aluno: {
        nome: 'Fabiano Oss',
        matricula: 100,
        media: 8.5
      },
      isShow: true,
      carros: [
        'Fusca', 'Chevette', 'Opala', 'Kombi'
      ],
      carros2: [
        {nome: 'Fusca', preco: 2500},
        {nome: 'Chevette', preco: 1000},
        {nome: 'Opala', preco: 5000}
      ],

      filtro: ''

    }
  },

  beforeMount() {
    console.log('before mount')
  },
  mounted() {
    console.log('mounted')
    this.updateDate()

  },


  methods: {
    updateDate() {
      this.data = new Date()
      let var1 = this.aluno.media
      var1--;

      /// const var2 = "teste"


      this.aluno.media = var1
    },
    adicionarCarro() {
      this.carros.push('Brasilia')
    },
    adicionarCarro2(carroP) {
      const novoCarro = {
        nome: carroP.nome,
        preco: carroP.preco
      }
      this.carros2.push(novoCarro)

      for(let i=0; i < this.carros2.length; i++) {
        console.log(this.carros2[i].nome)
      }

      this.carros2.forEach((c, idx) => {
        console.log(idx + ' ' + c.nome )
      })

    }

  },

  watch: {
    filtro: function(val) {
      console.log(val)
    }
  },
  computed: {
/*    marcaNome() {
      if (this.novoCarro.fabricante) {
        return (this.novoCarro.fabricante + ' ' + this.novoCarro.nome).split('').reverse().join('')
      }
      return ''
    }, */
    total() {
      /*let total = 0
      this.carros2.forEach(c => {
        total += c.preco
      })
      return total */
      // Map Reduce
      //console.log(this.carros2.map(c => c.preco))
      //console.log(this.carros2.map(c => c.nome))

      return this.carros2.map(c => c.preco).reduce((a, b) => a + b)

    },
    carrosFiltrados() {
      if (this.filtro != '') {
        return this.carros2.filter(c => {
            return c.nome.toUpperCase().startsWith(this.filtro.toUpperCase())
        })
      }
      return this.carros2
    }


  }


}
</script>

<style>

body {
  margin: 0 auto;
  max-width: 90vh;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  
  color: #2c3e50;
  margin-top: 60px;
  border: 1px solid silver;
  /** teste */
}
table {
  border-collapse: collapse;
}

table, th, td{
  border: 1px solid black;
}

.totalMaior10k {
  color: red;
}

.totalMaior20k {
  color: green;
}

</style>
