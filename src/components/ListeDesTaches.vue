<template>

  <div class="bloc__list">

    <h2 class="text-center">Tâches</h2>


      <Tache
          v-for="(task, index) in listeDesTaches" :key="index"
          :task="task"
          @changerEtatTache="changerEtatTache"
          @editerTache="editerTache"
          @supprimerTache="supprimerTache"
      ></Tache>
  </div>
</template>

<script>
import Tache from "./Tache.vue";

export default {
  name: 'ListeDesTaches',
  components: {Tache},

  props: {
    listeDesTaches: {
      type: Array,
      required: true
    },
  },

  methods: {
    changerEtatTache(task) {
      this.$emit("changerEtatTache", task);
    },
    editerTache(task) {
      this.$emit("editerTache", task);
    },
    supprimerTache(task) {
      this.$emit("supprimerTache", task);
    }
  }
}
</script>

<style scoped>

h2 {
  font-size: 1.2rem;
  font-weight: 600;
  width: 100%;
  background-color: #ffc023;
}

.bloc__list {
  min-height: 100px;
  max-height: 50vh;
  overflow: auto;
  border: 1px solid black;
  background-color: #e8e8e8;
  margin: 10px 0; padding-bottom: 32px;
  border-radius: 8px;
}


</style>