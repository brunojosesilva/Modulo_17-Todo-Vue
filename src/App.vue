<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cab.vue'
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';
  
  const estado = reactive({
    filtro: 'todas',
    tarefaNova: '',
    tarefas: [
      {
        titulo: 'Estudar',
        finalizada: false
      },
      {
        titulo: 'Limpar piscina',
        finalizada: true
      }
    ]
  })

  const getTarefaPendente = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTarefaFinalizada = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }

  const getTarefasFiltradas = () => {
    const filtro = estado.filtro;

    switch(filtro) {
      case 'pendente':
        return getTarefaPendente();
      case 'finalizadas':
        return getTarefaFinalizada();
      default: 
        return estado.tarefas;
    }
  }

  const cadastraTarefa = () => {
    const tarefaNova = {
      titulo: estado.tarefaNova,
      finalizada: false
    }
    estado.tarefas.push(tarefaNova);
    estado.tarefaNova = '';
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefasPendentes='getTarefaPendente().length' />
    <Formulario :tarefaNova="estado.tarefaNova" :editaTarefaNova="evento => estado.tarefaNova = eventos.target.value" :cadastraTarefa="cadastraTarefa()" />
    <ListaDeTarefas :tarefas="getTarefasFiltradas()" />
  </div>
</template>