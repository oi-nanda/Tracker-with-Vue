<template>
  <header>
    <h1>
      <img src="../assets/logo_tracker.png" id="logo_tracker" />
    </h1>
    <button class="button" @click="alterarTema">{{ textoBotao }}</button>
  </header>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "BarraLateral",
  emits: ["aoTemaAlterado"],
  data() {
    return {
      modoEscuroAtivo: false,
    };
  },
  computed:{
    textoBotao (){
      if(this.modoEscuroAtivo){
        return  'Desativar modo escuro'
      }
      return 'Ativar modo escuro'
    }
  },
  methods: {
    alterarTema() {
      this.modoEscuroAtivo = !this.modoEscuroAtivo;
      this.$emit("aoTemaAlterado", this.modoEscuroAtivo);
    },
  },
});
</script>

<style scoped>
header {
  padding: 1rem;
  justify-content: center;
  background: #4c2fa1;
  width: 100%;
  height: 100vh;
  text-align: center;
}

#logo_tracker {
  height: 100px;
  width: 100px;
}

.button {
  margin: 15px;
}

@media only screen and (max-width: 768px) {
  header {
    padding: 2.5rem;
    height: auto;
  }
}
</style>
