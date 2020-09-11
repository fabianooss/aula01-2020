<template>
    <form @submit.prevent="adicionarCarro()">

        <input type="text" placeholder="Informe o nome" required v-model="novoCarro.nome"/> <br>
        <input type="number" step="0.5" placeholder="Infome o valor" required v-model.number="novoCarro.preco"/> <br>

        <select v-model="novoCarro.fabricante">
            <option v-for="f in fabricantes" :key="f">{{f}}</option>
        </select>

        <br/>
        <label for="arCondicionado">Ar condicionado</label>
        <input type="checkbox" id="arCondicionado"  v-model="novoCarro.arCondicionado"/>

        <button type="submit">Adicionar</button>
    </form>  
</template>

<script>
export default {
    data() {
        return {
            novoCarro: {
                nome: '',
                preco: 0,
                fabricante: '',
                arCondicionado: false
            },
            fabricantes: ['VW', 'GM', 'BMW'],
        }
    },
    methods: {
        adicionarCarro() {
            // validações
            this.$emit('adicionar', this.novoCarro)
        }
    }

}
</script>

<style>

</style>