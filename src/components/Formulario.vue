<script setup>
    const props = defineProps(['cadastraTarefa','tarefaNova', 'editaTarefaNova', 'trocarFiltro' ]);
</script>
<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input required type="text" placeholder="Digite aqui a sua tarefa" class="form-control" :value="props.tarefaNova" @change="props.editaTarefaNova">
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select class="form-control" @change="props.trocarFiltro">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>