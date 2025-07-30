<script setup>
// Definindo as props que o componente vai receber
const props = defineProps({
  tarefas: {
    type: Array,
    required: true
  }
})

const alternarTarefa = (tarefa) => {
  tarefa.finalizada = !tarefa.finalizada
}
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefas" :key="tarefa.titulo">
            <input :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" @change="alternarTarefa(tarefa)">
            <label :class="{ 'done': tarefa.finalizada }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
    color: gray;
}
</style>