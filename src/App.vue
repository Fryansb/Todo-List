<script setup>
import { reactive } from 'vue'

const estado = reactive({
  filtro: 'todas',
  tarefaTemporaria: '',
  tarefas: [
    {
      titulo: 'Estudar Vue.js',
      concluida: false
    },
    {
      titulo: 'Estudar JavaScript',
      concluida: false
    },
    {
      titulo: 'Estudar HTML',
      concluida: false
    }
  ]
})

const alternarTarefa = (tarefa) => {
  tarefa.concluida = !tarefa.concluida
}

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.concluida)
}

const getTarefasConcluidas = () => {
  return estado.tarefas.filter(tarefa => tarefa.concluida)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'concluidas':
      return getTarefasConcluidas();
    default:
      return estado.tarefas;
  }
}

const cadastrarTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTemporaria,
    concluida: false
  }

  estado.tarefas.push(tarefaNova);
  estado.tarefaTemporaria = '';
}
  

</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
      Você possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa">
      <div class="row">
        <div class="col">
          <input :value="estado.tarefaTemporaria" @change="evento => estado.tarefaTemporaria = evento.target.value" required type="text" placeholder="Digite uma tarefa" class="form-control" />
        </div>
        <div class="col-md-1">
          <button type="submit" class="btn btn-primary">Adicionar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="concluidas">Tarefas concluídas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()" >
        <input :checked="tarefa.concluida" :id="tarefa.titulo" type="checkbox" @change="alternarTarefa(tarefa)" >
        <label :class="{'done': tarefa.concluida}" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
          
        </label>
      </li>

    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
    color: gray;
  }
</style>
