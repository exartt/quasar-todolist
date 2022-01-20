<template>
  <div class="q-pa-md">
    <div class="q-gutter-y-md column" style="max-width: 300px" v-for="tarefa in tarefas" :key="tarefa.text">
      <q-input clearable filled color="purple-12" v-model="tarefa.text" label="Label" />
      <q-input
        clearable
        clear-icon="close"
        filled
        color="purple-12"
        v-model="tarefa.text"
        label="Label"
      />
    </div>
    <div class="q-gutter-md" style="max-width: 500px">
      <q-input outlined v-model="novaTarefa" label="Descrição" />
      <q-btn
        @click="gerarTarefa"
        v-bind="size" :key="`btn_size_round_${size}`"
        round
        color="primary"
        :size="size"
        :icon="icon"
      />
    </div>
  </div>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      novaTarefa: '',
      tarefas: [],
      size: 'md',
      icon: 'add_a_photo'
    }
  },
  methods: {
    gerarTarefa () {
      const index = this.tarefas.findIndex(tarefa => tarefa.text === this.novaTarefa)
      if (index === -1) {
        this.tarefas.push({
          text: this.novaTarefa,
          checked: false
        })
      } this.novaTarefa = ''
    }
  }
}
</script>
