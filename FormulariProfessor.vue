/* eslint-disable */
<template>

  <form @submit.prevent="addProfessor">

    <label>Nom</label>
    <input type="text" v-model="nom" placeholder="Nom">
    <br><br>

    <label>Cognoms</label>
    <input type="text" v-model="cognoms" placeholder="Cognoms">
    <br><br>

    <label>DNI</label>
    <input type="text" v-model="dni" placeholder="DNI">
    <br><br>

    <label>Skills</label><br>
    <input type="checkbox" value="Base de Dades" v-model="skills"> Base de Dades<br>
    <input type="checkbox" value="Sistemes" v-model="skills"> Sistemes<br>
    <input type="checkbox" value="Desenvolupament Web" v-model="skills"> Desenvolupament Web<br>
    <input type="checkbox" value="Seguretat Cloud" v-model="skills"> Seguretat Cloud<br><br>

    <input type="checkbox" v-model="docs"> Documentació entregada
    <br><br>

    <button type="submit">{{ editIndex === null ? 'Afegir' : 'Actualitzar' }}</button>
  </form>

  <hr>

  <table>
    <thead>
      <tr>
        <th>Nom</th>
        <th>Cognoms</th>
        <th>DNI</th>
        <th>Skills</th>
        <th>Docs</th>
        <th>Accions</th>
      </tr>
    </thead>

    <tbody>
      <tr v-for="(p, i) in professors" :key="i">
        <td>{{ p.nom }}</td>
        <td>{{ p.cognoms }}</td>
        <td>{{ p.dni }}</td>
        <td>{{ p.skills.join(', ') }}</td>
        <td>{{ p.docs ? 'Sí' : 'No' }}</td>
        <td>
          <button @click="editarElProfessor(i)">Editar</button>
          <button @click="esborrarProfessor(i)">Eliminar</button>
        </td>
      </tr>
    </tbody>
  </table>

</template>

<script setup>
import { ref } from 'vue'

const nom = ref('')
const cognoms = ref('')
const dni = ref('')
const skills = ref([])
const docs = ref(false)

const professors = ref([])
const editIndex = ref(null)

function addProfessor () {
  const professorData = {
    nom: nom.value,
    cognoms: cognoms.value,
    dni: dni.value,
    skills: [...skills.value],
    docs: docs.value
  }

  if (editIndex.value === null) {
    professors.value.push(professorData)
  } else {
    professors.value[editIndex.value] = professorData
    editIndex.value = null
  }

  reiniciarFormulari()
}

function editarElProfessor (index) {
  const p = professors.value[index]

  nom.value = p.nom
  cognoms.value = p.cognoms
  dni.value = p.dni
  skills.value = [...p.skills]
  docs.value = p.docs

  editIndex.value = index
}

function esborrarProfessor (index) {
  professors.value.splice(index, 1)
}

function reiniciarFormulari () {
  nom.value = ''
  cognoms.value = ''
  dni.value = ''
  skills.value = []
  docs.value = false
}
</script>

<style scoped>

</style>
