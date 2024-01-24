<template>
  <main
    class="columns is-gapless is-multiline"
    :class="{ 'modo-escuro': modoEscuroAtivo }"
  >
    <!-- caso o modoEscuroAtivo for true ele adiciona a classe 'modo-escuro'-->
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="trocarTema" />
    </div>
    <div class="column is-three-quarter conteudo">
      <FormularioTracker @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <TarefaTracker
          v-for="(tarefa, index) in tarefas"
          :key="index"
          :tarefa="tarefa"
        />
        <BoxTracker v-if="listaEstaVazia">
          Você não está muito produtivo hoje... :(
        </BoxTracker>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import BarraLateral from "./components/BarraLateral.vue";
import FormularioTracker from "./components/Formulario.vue";
import TarefaTracker from "./components/Tarefa.vue";
import ITarefa from "./interfaces/ITarefa";
import BoxTracker from "./components/Box.vue";

export default defineComponent({
  name: "App",
  components: {
    BarraLateral,
    FormularioTracker,
    TarefaTracker,
    BoxTracker,
  },
  data() {
    return {
      tarefas: [] as ITarefa[],
      modoEscuroAtivo: false,
    };
  },
  computed: {
    listaEstaVazia(): boolean {
      return this.tarefas.length === 0;
    },
  },
  methods: {
    salvarTarefa(tarefa: ITarefa) {
      this.tarefas.push(tarefa);
    },
    trocarTema(modoEscuroAtivo: boolean) {
      this.modoEscuroAtivo = modoEscuroAtivo;
    },
  },
});
</script>

<style>
.lista {
  padding: 1.25rem;
}

main {
  --bg-primario: #fff;
  --text-primario: #000;
}

main.modo-escuro {
  --bg-primario: #1a0735;
  --text-primario: #ddd;
}

.conteudo {
  background-color: var(--bg-primario);
}
</style>
