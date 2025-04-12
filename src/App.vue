<script lang="ts" setup>
import { ref } from 'vue'
import axios from 'axios'
const universes = ref([])
const superheroes = ref([])
const genders = ref([])
const universe = ref([])
const superhero = ref([])
const gender = ref([])
async function getUniverses() {
  const response = await axios.get('http://127.0.0.1:8000/api/universes/')
  universes.value = response.data
}
async function getSuperheroes() {
  const response = await axios.get('http://127.0.0.1:8000/api/superheroes')
  superheroes.value = response.data
}
async function getGenders() {
  const response = await axios.get('http://127.0.0.1:8000/api/genders')
  genders.value = response.data
}
async function getUniverse(name: string) {
  const response = await axios.get(`http://127.0.0.1:8000/api/universes/${name}`)
  universe.value = response.data
  console.log(response.data)
}
async function getSuperheroe(name: string) {
  const response = await axios.get(`http://127.0.0.1:8000/api/superheroes/${name}`)
  superhero.value = response.data
  console.log(response.data)
}
async function getGender(id: string) {
  const response = await axios.get(`http://127.0.0.1:8000/api/genders/${id}`)
  gender.value = response.data
  console.log(response.data)
}
</script>

<template>
  <div style="display: flex">
    <div>
      <div style="padding: 2px; margin: 10px">
        <h2>Universes</h2>
        <button @click="getUniverses">Get Universes</button>
        <div v-for="(universe, index) in universes" :key="index">
          <p>Id: {{ universe.id }}</p>
          <p>Name: {{ universe.name }}</p>
        </div>
      </div>
      <div style="padding: 2px; margin: 10px">
        <h2>Universe</h2>
        <input type="text" v-model="universeName" placeholder="Enter Universe name" />
        <button @click="getUniverse(universeName)">Get Universe</button>
        <div v-for="(universe, index) in universe" :key="index">
          <p>Id: {{ universe.id }}</p>
          <p>Name: {{ universe.name }}</p>
        </div>
      </div>
    </div>
    <div>
      <div style="padding: 2px; margin: 10px">
        <h2>Superheroes</h2>
        <button @click="getSuperheroes">Get Superheroes</button>
        <div v-for="(superhero, index) in superheroes" :key="index">
          <p>Name: {{ superhero.name }}</p>
          <p>Universe: {{ superhero.universo_id }}</p>
          <p>Publisher: {{ superhero.publisher }}</p>
          <p>Real Name: {{ superhero.real_name }}</p>
          <p>Gender: {{ superhero.genero_id }}</p>
        </div>
      </div>
      <div>
        <h2>SuperHero</h2>
        <input type="text" v-model="superheroName" placeholder="Enter Superhero name" />
        <button @click="getSuperheroe(superheroName)">Get Superhero</button>
        <div v-for="(superhero, index) in superhero" :key="index">
          <p>Id: {{ superhero.id }}</p>
          <p>Name: {{ superhero.name }}</p>
          <p>Universe: {{ superhero.universo_id }}</p>
          <p>Publisher: {{ superhero.publisher }}</p>
          <p>Real Name: {{ superhero.real_name }}</p>
          <p>Gender: {{ superhero.genero_id }}</p>
        </div>
      </div>
    </div>
    <div style="padding: 2px; margin: 10px">
      <h2>Gender</h2>
      <button @click="getGenders">Get Gender</button>
      <div v-for="(gender, index) in genders" :key="index">
        <p>Id: {{ gender.id }}</p>
        <p>Name: {{ gender.name }}</p>
      </div>
      <div>
        <h2>Gender</h2>
        <input type="text" v-model="genderName" placeholder="Enter id gender" />
        <button @click="getGender(genderName)">Get Gender</button>
        <div v-for="(gender, index) in gender" :key="index">
          <p>Id: {{ gender.id }}</p>
          <p>Name: {{ gender.name }}</p>
        </div>
      </div>
    </div>
  </div>
</template>
