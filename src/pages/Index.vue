<template>
  <q-page class="q-pa-md bg-grey-3">
    <div class="row items-center justify-center rounded-borders full-width q-mb-lg">
      <q-input bg-color="white" dense rounded outlined placeholder="pesquisar" v-model="filtroTarefa" style="width: 60vw">
        <template v-slot:append>
          <q-icon name="search" />
        </template>
      </q-input>
    </div>
    <div class="column items-center full-width">
      <div :class="tarefa.checked ? isChecked[1] : isChecked[0]" style="max-width: 60vw" v-for="tarefa in filterTarefas" :key="tarefa.text">
        <div class="tarefa.checked ? col-auto">
          <q-checkbox :value="tarefa.checked" @input="tarefa.checked = !tarefa.checked" />
        </div>
        <div :class="tarefa.checked ? 'text-strike col-6' : 'col-6'" >{{ tarefa.text }}</div>
        <div class="col-auto">
          <q-btn icon="delete" flat round @click="excluirTarefa(tarefa)"/>
        </div>
      </div>
    </div>
    <q-page-sticky position="bottom-right">
      <div class="row items-center q-gutter-sm q-pb-md q-pr-md">
        <div class="col-auto">
          <q-input
            bg-color="white"
            dense
            rounded
            style="min-width: 300px"
            outlined
            v-model="novaTarefa"
            label="Descrição"
            @keyup.enter="gerarTarefa"
          />
        </div>
        <div class="col-auto">
          <q-btn round color="blue" @click="gerarTarefa" icon="add"/>
        </div>
      </div>
    </q-page-sticky>
  </q-page>
</template>

<script>
export default {
  name: 'PageIndex',
  data () {
    return {
      filtroTarefa: '',
      novaTarefa: '',
      tarefas: [
        {
          text: 'Ir na padaria',
          checked: false
        },
        {
          text: 'Ir no açougue',
          checked: false
        },
        {
          text: 'Ir na disney',
          checked: false
        }
      ],
      isChecked: [
        'row items-center bg-white justify-between shadow-3 rounded-borders full-width q-mt-sm',
        'row items-center justify-between shadow-3 rounded-borders full-width q-mt-sm',
        'text-strike'
      ]
    }
  },
  computed: {
    filterTarefas () {
      return this.tarefas.filter(
        (tarefa) => tarefa.text.toLocaleLowerCase().match(this.filtroTarefa.toLowerCase())
      )
    }
  },
  methods: {
    excluirTodaTarefa () {
      this.tarefas = []
    },
    gerarTarefa () {
      const index = this.tarefas.findIndex((tarefa) => {
        return this.novaTarefa === tarefa.text
      })
      console.log(index)
      if (this.novaTarefa !== '') {
        if (index === -1) {
          this.tarefas.push({
            text: this.novaTarefa,
            checked: false
          })
          this.novaTarefa = ''
        } else {
          alert('Ocorreu um erro, já existe um item igual na sua lista!')
        }
      }
    },
    excluirTarefa (tarefa) {
      this.tarefas = this.tarefas.filter((t) => {
        return t.text !== tarefa.text
      })
    }
  }
}
</script>
