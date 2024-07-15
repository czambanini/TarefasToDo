<template>
	<div id="app">
		<h1>Lista de Tarefas</h1>

		<progress-bar :progresso="carregamento"/>
		<new-input :tarefas="tarefas" @novaTarefa="atualizarLista"/>
		<cards-grid :tarefas="tarefas" @atualizarlista="atualizarLista"/>

	</div>
</template>

<script>
import CardsGrid from './components/CardsGrid.vue'
import NewInput from './components/NewInput.vue';
import ProgressBar from './components/ProgressBar.vue'

export default {
	components: { CardsGrid, ProgressBar, NewInput },
	data() {
		return {
			tarefas: [],
			carregamento: 0
		}
	},
	watch: {
		//mudou tarefas para objetos e definiu deep e handler para que as tarefas sejam monitoradas mais a fundo (mudanças internas)
		tarefas: {
			deep: true,
			handler() {
				localStorage.setItem('tarefas', JSON.stringify(this.tarefas))
			}
		}
	},
	methods: {
		calcularStatus(tarefas) {
            let totalTarefas = 0
            let tarefasConcluidas = 0
            tarefas.forEach(tarefa => {
                totalTarefas += 1
                if (!tarefa.ativa) tarefasConcluidas += 1
            });

			this.carregamento = totalTarefas === 0 ? 0 : (tarefasConcluidas * 100 / totalTarefas);
        },
		atualizarLista(tarefasAtualizadas) {
			this.tarefas = tarefasAtualizadas
			this.calcularStatus(this.tarefas);
		}
    },
	created() {
		const json = localStorage.getItem('tarefas')
		const array = JSON.parse(json)
		this.tarefas = Array.isArray(array) ? array : []
	}
}
</script>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Ubuntu+Sans:ital,wght@0,100..800;1,100..800&display=swap');

	body {
		font-family: "Ubuntu Sans", sans-serif;
		background: linear-gradient(90deg, rgba(170,245,230,1) 0%, rgba(215,230,224,1) 45%, rgba(147,201,218,1) 100%);
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		min-height: 100vh;
		gap: 50px;
	}

	#app h1 {
		margin-bottom: 5px;
		margin-top: 30px;
		font-weight: 500;
		font-size: 3rem;
		text-shadow: 2px 2px 5px #a6babc;
	}
</style>
