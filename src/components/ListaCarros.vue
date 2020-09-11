<template>
    <div>
        <ul>
            <li v-for="c in carros" :key="c"> {{c}} </li>
        </ul>
    </div>
</template>

<script>
export default {
    // name: 'ListaCarros',
    props: {
        carros: Array
    },

    // props:['carros']


}
</script>

<style>

</style>