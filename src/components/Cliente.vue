<template>
    <div :class="{'cliente': !isPremium, 'cliente-premium': isPremium}">
        <h4>Nome: {{ cliente.nome }}</h4>
        <hr>
        <p>Email: {{ cliente.email }}</p>
        <p v-show="cliente.idade > 30">Idade: {{ cliente.idade }}</p>
        <button @click="mudarCor()"> Mudar Cor</button>
        <button @click="emitirEventoDelete" style="margin-left: 2px;">Deletar</button>
    </div>
</template>

<script>
export default {
    data(){
        return {
            isPremium : false
        }
    },
    props:{
        cliente: Object
    },
    methods: {
        mudarCor : function() { 
            this.isPremium = !this.isPremium;
        },
        emitirEventoDelete: function() {
            console.log('Emitindo do filho!');
            this.$emit('meDelete',{clienteData: this.cliente.id});
        }
    }
}
</script>

<style scoped>
    .cliente {
        color: chocolate;
        height: 180px;
        width: 600px;
        background-color: rgba(139, 139, 139, 0.363);
        padding: 1%;
        margin-top: 1.1%;
    }
    .cliente-premium {
        color: goldenrod;
        height: 180px;
        width: 600px;
        background-color: black;
        padding: 1%;
        margin-top: 1.1%;
    }
</style>