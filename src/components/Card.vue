<template>
<div class="card" :class="cardClass" @click="clicarTarefa">
    <div class="titulo">
        <i class="pi pi-times-circle icon" @click="deletarTarefa"></i>
        {{ name }}
    </div>
</div>
</template>
  
<script>
import 'primeicons/primeicons.css'

export default {
    name: 'Card',
    data() {
        return {
        }
    },
    props: {
        name: {
        type: String,
        required: true
        },
        ativa: {
        type: Boolean,
        required: true
        }
    },
    methods: {
        clicarTarefa() {
            this.$emit('clicarTarefa');
        },
        deletarTarefa() {
            this.$emit('deletarTarefa');
        }
    },
    computed: {
        cardClass() {
            return {
                cardAtivo: this.ativa,
                cardConcluido: !this.ativa
            }
        }
    }
}
</script>

<style scopeed>
.card {
    width: 200px;
    height: 120px;
    border-radius: 15px;
    margin: 10px;
    padding: 15px;
    box-shadow: rgba(99, 99, 99, 0.2) 0px 2px 8px 0px;
    position: relative;
    cursor: pointer;
    text-align: center;
}

.cardAtivo {
    background-color: #f3f3f3;
    color: #363636;
}

.cardConcluido {
    background-color: #8dd597;
    text-decoration: line-through;
}

.titulo {
    font-size: 23px;
    font-weight: 400;
    margin: auto;
}

.icon {
    font-size: 15px;
    position:absolute;
    top: 7px;
    right: 7px;
}
</style>
