<template>
    <div class="box-tarefas">
        <card v-for="tarefa in tarefas" :key="tarefa.name"
            :name="tarefa.name"
            :ativa="tarefa.ativa"
            @clicarTarefa="clicarTarefa(tarefa)"
            @deletarTarefa="deletarTarefa(tarefa)"
        />
    </div> 
</template>
    
<script>
import Card from './Card.vue'

export default {
    name: 'ListaTarefas',
    components: { Card },
    props: {
        tarefas: {
        type: Array,
        required: true
        }
    },
    methods: {
        clicarTarefa(tarefa) {
            tarefa.ativa = !tarefa.ativa;
            this.$emit('atualizarlista', this.tarefas);
        },
        deletarTarefa(tarefaDeletada) {
            this.tarefas = this.tarefas.filter(tarefa => tarefa.name !== tarefaDeletada.name)
            this.$emit('atualizarlista', this.tarefas);
        }
    }
}
</script>

<style scopeed>
.box-tarefas {
    display:flex;
    flex-wrap: wrap;
    justify-content: center;
    margin-top: 40px;
}

.mensagemErro {
    color: #ea3232;
    font-style: italic;
    font-size: 14px;
    margin-top: 5px;

}

</style>