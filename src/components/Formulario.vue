<script setup>
const props = defineProps({
  cadastraTarefa: {
    type: Function,
    required: true
  },
  tarefaTemp: {
    type: String,
    required: true
  },
  trocarFiltro: {
    type: Function,
    required: true
  },
  editaTarefaTemp: {
    type: Function,
    required: true
  }
})
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa">
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTemp" @change="props.editaTarefaTemp" required
                    type="text" placeholder="Digite a descrição da sua tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>