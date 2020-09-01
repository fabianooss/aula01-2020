<template>
  <div id="app">

    <h1 :title="dica" v-if="isShow"> {{tituloAula}} - v-if</h1>
    <h1 :title="dica" v-show="isShow"> {{tituloAula}} - v-show</h1>
    <p> {{data}} </p>

    <p> {{aluno.nome}} </p>
    <p> {{aluno.media + 1}} </p>

    <ul>
      <li v-for="c in carros" :key="c"> {{c}} </li>
    </ul>


    <hr/>

    <form @submit.prevent="adicionarCarro2()">
      <span v-show="novoCarro.fabricante != null"> {{novoCarro.fabricante + ' ' + novoCarro.nome}}<br/>  </span>
      {{ marcaNome }} <br/>

      <input type="text" placeholder="Informe o nome" required v-model="novoCarro.nome"/> <br>
      <input type="number" step="0.5" placeholder="Infome o valor" required v-model.number="novoCarro.preco"/> <br>

      <select v-model="novoCarro.fabricante">
        <option v-for="f in fabricantes" :key="f">{{f}}</option>

      </select>

      <label for="arCondicionado">Ar condicionado</label>
      <input type="checkbox" id="arCondicionado"  v-model="novoCarro.arCondicionado"/>

      <button type="submit">Adicionar</button>
    </form>

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

export default {

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
      novoCarro: {
        nome: '',
        preco: null,
        fabricante: null,
        arCondicionado: false
      },
      fabricantes : ['VW', 'GM', 'BMW'],
      filtro: ''

    }
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
    adicionarCarro2() {
      const novoCarro = {
        nome: this.novoCarro.nome,
        preco: this.novoCarro.preco
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

  computed: {
    marcaNome() {
      if (this.novoCarro.fabricante) {
        return (this.novoCarro.fabricante + ' ' + this.novoCarro.nome).split('').reverse().join('')
      }
      return ''
    },
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
