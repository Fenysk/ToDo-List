<template>
  <article
      class="task"
      :class="task.state ? 'task--done' : ''"
  >
    <i
        class="mr-2"
        :class="task.state ? 'fas fa-check-square' : 'far fa-square'"
        @click="changerEtatTache(task)"
    ></i>

    <p>{{ task.name }}</p>

    <span class="ml-auto">{{ task.date.getHours() }}:{{ task.date.getMinutes() }}</span>

    <i
        class="fas fa-pen-to-square ml-2"
        @click="editerTache(task)"
    ></i>
    <i
        class="fas fa-trash ml-2"
        @click="supprimerTache(task)"
    ></i>
  </article>
</template>

<script>
export default {
  name: "Tache",

  props: {
    task: {
      type: Object,
      required: true
    }
  },

  methods: {
    changerEtatTache(task) {
      this.$emit("changerEtatTache", task);
      console.log(task.name)
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

input {
  margin-right: 10px;
  margin-top: auto;
  margin-bottom: auto;
  cursor: pointer;
}

.task{
  padding: 5px 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  margin: 6px 8px;
  background-color: #fff;

  display: flex;
  flex-flow: row nowrap;
  align-items: center;
}

.task--done p {
  text-decoration: line-through;
  color: #8c8ea4;
}

.task--done:first-child{
  margin-top: 18px !important;
}


i {
  cursor: pointer;
}

i.fa-check-square {
  color: #8c8ea4;
}

i.fa-square {
  color: #0613ad;
}

i.fa-pen-to-square {
  color: #096703;
}

i.fa-trash {
  color: #6e0303;
}

i.fa-pen-to-square:hover {
  color: #0f8f07;
}

i.fa-trash:hover {
  color: #d01402;
}

</style>