<script setup>
import { reactive } from 'vue';

  
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
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Você possui {{ getTarefaPendente().length }} tarefas pendentes.
      </p>
    </header>
    <form @submit.prevent="cadastraTarefa">
        <div class="row">
          <div class="col">
            <input required type="text" placeholder="Digite aqui a sua tarefa" class="form-control" @change="evento => estado.tarefaNova = evento.target.value">
          </div>
          <div class="col-md-1">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
          </div>
          <div class="col-md-2">
            <select class="form-control" @change="evento => estado.filtro = evento.target.value">
              <option value="todas">Todas tarefas</option>
              <option value="pendentes">Pendentes</option>
              <option value="finalizadas">Finalizadas</option>
            </select>
          </div>
        </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
        <input type="checkbox" :checked="tarefa.finalizada" :id="tarefa.titulo" @change="evento => tarefa.finalizada = evento.target.checked">
        <label class="ms-3" :for="tarefa.titulo" :class="{done: tarefa.finalizada}">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
