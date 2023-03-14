<template>

  <div class="app">
    <h1>Ma ToDo List</h1>

    <div class="bloc__gestation">
      <form @submit.prevent="ajouterTache">
        <input
            type="text"
            placeholder="Nom de la tâche"
            v-model="nomTache"
        >
        <button
            type="button"
            @click="ajouterTache"
        >Ajouter
        </button>
      </form>

      <form
          class="flex flex-row"
          @submit.prevent="filtrerTaches">

        <input
            type="text"
            placeholder="Filtres"
            v-model="termesFiltre"
        >

        <button
            class="button button--green"
            type="button"
            @click="filtrerTaches"
        >
          Filtrer
        </button>

        <button
            class="button button--red"
            type="button"
            @click="supprimerFiltres"
        >
          <i class="fas fa-times"></i>
        </button>

      </form>
    </div>

    <ListeDesTaches
        :liste-des-taches="filtreActif ? listeDesTachesFiltrees : listeDesTachesTriees"
        @editerTache="editerTache"
        @supprimerTache="supprimerTache"
        @changerEtatTache="changerEtatTache">
    </ListeDesTaches>

    <div class="flex float-right">

      <button
          class="button button--orange"
          type="button"
          @click="viderListeDesTachesTerminees"
      >
        <p>Supprimer les tâches terminées</p>
        <i class="fas fa-trash-alt"></i>
      </button>

      <button
          class="button button--red"
          type="button"
          @click="toutSupprimer"
      >
        <p>Tout supprimer</p>
        <i class="fas fa-trash-alt"></i>
      </button>
    </div>

  </div>

</template>

<script>

import ListeDesTaches from "./components/ListeDesTaches.vue";

export default {
  name: 'App',
  components: {ListeDesTaches},

  data() {
    return {
      nomTache: '',

      termesFiltre: '',

      filtreActif: false,

      listeDesTaches: [
        {
          date: new Date('2020-01-01 12:45:45'),
          name: 'Faire les courses',
          state: false,
        },
        {
          date: new Date('2020-01-01 19:24:45'),
          name: 'Appeler Mamie',
          state: false,
        },
        {
          date: new Date('2020-01-01 20:45:45'),
          name: 'Faire le ménage',
          state: false,
        },
        {
          date: new Date('2020-01-01 21:45:45'),
          name: 'Aller à la salle',
          state: true,
        },
        {
          date: new Date('2020-01-01 22:45:45'),
          name: 'Faire la lessive',
          state: true,
        },
      ],
    }
  },

  computed: {
    listeDesTachesTriees() {
      return this.listeDesTaches.sort(
          (a, b) => a.state - b.state
      )
    },

    listeDesTachesFiltrees() {
      return this.listeDesTaches.filter(task => task.name.includes(this.termesFiltre))
    },

  },

  methods: {
    ajouterTache() {
      if (this.nomTache !== '' && this.nomTache.slice(0, 1) !== ' ') {
        this.listeDesTaches.push({
          date: new Date(),
          name: this.nomTache,
          state: false,
        })
        this.nomTache = ''
      }
    },

    changerEtatTache(task) {
      task.state = !task.state
    },

    editerTache(task) {
      this.nomTache = task.name
      this.supprimerTache(task)
    },

    supprimerTache(task) {
      this.listeDesTaches.splice(this.listeDesTaches.indexOf(task), 1)
    },

    viderListeDesTachesTerminees() {
      this.listeDesTaches = this.listeDesTaches.filter(task => !task.state)
    },

    toutSupprimer() {
      this.listeDesTaches = []
    },

    filtrerTaches() {
      this.filtreActif = true
    },

    supprimerFiltres() {
      this.filtreActif = false
      this.termesFiltre = ''
    },

  }
}

</script>

<style>

.app {
  padding: 20px;
  max-width: 600px;
  margin: auto;
}

h1 {
  text-align: center;
  font-size: 2em;
  font-weight: bold;
  margin-bottom: 20px;
}

.bloc__gestation {
  display: flex;
  flex-flow: column;
}

input {
  width: auto;
  padding: 10px;
  border: 2px solid #084b00;
  border-radius: 5px;
  margin-bottom: 10px;
}

button {
  padding: 10px;
  color: white;
  font-weight: bold;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin-bottom: 10px;
  margin-left: 10px;
  background-color: #228c06 !important;
}

.button--red {
  background-color: #be0000 !important;
  padding: 8px 16px;
}

.button--orange {
  background-color: #fa700f !important;
  padding: 8px 16px;
}

.button--green p {
  width: auto;
  margin-right: 10px;
}

.button {
  display: flex;
  flex-flow: row;
  align-items: center;
}

.button.button--red:hover > p {
  width: 124px;
  margin-right: 10px;
  transition: all 0.3s ease;
}

.button.button--orange:hover > p {
  width: 250px;
  margin-right: 10px;
  transition: all 0.3s ease;
}

.button p {
  transition: all 0.3s ease;
  width: 0;
  overflow: hidden;
  white-space: nowrap;
}

</style>