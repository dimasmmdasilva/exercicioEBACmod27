<template>
    <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>Você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>
    </header>
    <form @submit.prevent="cadastraTarefa">
        <div class="row">
        <div class="col">
            <input v-model="estado.tarefaTemp" required type="text" placeholder="Digite a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-1">
            <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
            <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
            </select>
        </div>
        </div>
    </form>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()" :key="tarefa.título">
        <input @change="evento => tarefa.finalizadas = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.título" type="checkbox">
        <label :class="{ done: tarefa.finalizadas }" class="ms-3" :for="tarefa.título">
            {{ tarefa.título }}
        </label>
        </li>
    </ul>
    </div>
</template>

<script setup>
import { reactive } from 'vue';

const estado = reactive
({
    filtro: 'todas',
    tarefaTemp: '',
    tarefas: [
    { título: 'Estudar VueJS', finalizada: false },
    { título: 'Caminhada na rua', finalizada: false },
    { título: 'Treinamento físico', finalizada: false },
    ],
});

const getTarefasPendentes = () =>
{
    return estado.tarefas.filter(tarefa => !tarefa.finalizada);};

const getTarefasFinalizadas = () =>
{
    return estado.tarefas.filter(tarefa => tarefa.finalizada);
};
const getTarefasFiltradas = () =>
{
const { filtro } = estado;
    switch (filtro)
    {
        case 'pendentes':
            return getTarefasPendentes();
        case 'finalizadas':
            return getTarefasFinalizadas();
        default:
            return estado.tarefas;
    }
};

const cadastraTarefa = () =>
{
    const tarefaNova = {
    título: estado.tarefaTemp,
    finalizada: false,
    };
    estado.tarefas.push(tarefaNova);
    estado.tarefaTemp = '';
};
</script>

<style scoped>
.done
{
    text-decoration: line-through;
}
</style>
