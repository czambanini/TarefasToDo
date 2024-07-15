<template>
    <div class="new-input">
        <div>
            <input
                @keyup="valor = $event.target.value" 
                @keydown="erroNomeDuplicado = false"
                type="text" 
                placeholder="Nome da tarefa"
                :value = "valor"
            />
            <button @click="criarTarefa">+</button>
        </div>
        <div v-if="erroNomeDuplicado">
            <p class="mensagem-erro">Essa task já existe. Tente outro nome.</p>
        </div>
    </div>
</template>
    
<script>
export default {
    name: 'NewInput',
    data() {
        return {
            valor: '',
            erroNomeDuplicado: false
        }
    },
    props: {
        tarefas: {
        type: Array,
        required: true
        }
    },
    methods: {
        criarTarefa(){
            let nomeDuplicado = false
            this.tarefas.forEach(tarefa => {
                if(tarefa.name === this.valor) nomeDuplicado = true
            });
            if(nomeDuplicado === false) {
                this.tarefasAtualizadas = [...this.tarefas, { name: this.valor, ativa: true }]
                this.valor = ''
                this.$emit('novaTarefa', this.tarefasAtualizadas);
            } else {
                this.erroNomeDuplicado = true
            }
        }
    }
}
</script>

<style scopeed>
.new-input {
    display: flex;
    flex-direction: column;
    width: 100%;
}

input {
    padding-left: 10px;
    height: 30px;
    width: 300px;
    border: 1px solid #474747;
    border-radius: 8px 0 0 8px;
}

input:focus {
    outline: 0;
    color: #5a5a5a;
    border: 1px solid #474747;
}

button {
    height: 34px;
    width: 34px;
    margin-left: -2px;
    color: #fff;
    font-size: 20px;
    background-color: rgb(113, 174, 228);
    border: 1px solid #474747;
    border-radius: 0 8px 8px 0;
}

.mensagem-erro {
    color: #ea3232;
    font-style: italic;
    font-size: 14px;
    margin-top: 5px;

}

</style>