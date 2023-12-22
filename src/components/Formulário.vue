<script setup>
const props = defineProps(['tarefaTemp']);
const emits = ['trocar-filtro', 'edita-tarefa-temp', 'cadastra-tarefa'];
</script>

<template>
    <form @submit.prevent="$emit('cadastra-tarefa')">
        <div class="row">
            <div class="col">
                <input v-model="props.tarefaTemp" @change="$emit('edita-tarefa-temp', $event)" required type="text" placeholder="Digite a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-1">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="$emit('trocar-filtro', $event)" class="form-control">
                    <option value="todas">Todas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>
