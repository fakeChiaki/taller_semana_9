<template>
    <section>
      <nav>
        <ul>
          <li><button @click="handleClick(0)">Población de Países</button></li>
          <li><button @click="handleClick(1)">Recomendaciones de Anime</button></li>
          <li><button @click="handleClick(2)">Anime Aleatorio</button></li>
          <li><button @click="handleClick(3)">Manga Aleatorio</button></li>
        </ul>
      </nav>

      <main>
        <section v-if="apiData" class="data-section">
          <h2>Resultado</h2>
          <pre>{{ apiData }}</pre>
        </section>

        <section v-if="apiError" class="error-section">
          <h2>Error</h2>
          <p>{{ apiError }}</p>
        </section>
      </main>
    </section>
  </template>

<script setup>
  import { ref } from 'vue'
  import axios from 'axios'

  const apiData = ref(null)
  const apiError = ref(null)

  const endpoints = [
    'https://countriesnow.space/api/v0.1/countries/population',
    'https://api.jikan.moe/v4/recommendations/anime',
    'https://api.jikan.moe/v4/random/anime',
    'https://api.jikan.moe/v4/random/manga'
  ]

  const handleClick = async (endpointIndex) => {
    resetState()

    try {
      const response = await axios.get(endpoints[endpointIndex])
      apiData.value = response.data
    } catch (err) {
      apiError.value = 'Error al obtener datos: ' + err.message
    }
  }

  const resetState = () => {
    apiData.value = null
    apiError.value = null
  }
  </script>

<style scoped>
  section {
    padding: 20px;
    font-family: Arial, sans-serif;
  }

  header h1 {
    text-align: center;
    color: #2c3e50;
  }

  nav ul {
    display: flex;
    justify-content: center;
    list-style-type: none;
    padding: 0;
  }

  nav ul li {
    margin: 0 10px;
  }

  button {
    background-color: #3498db;
    color: white;
    padding: 12px 24px;
    border: none;
    border-radius: 8px;
    cursor: pointer;
    font-size: 16px;
    transition: background-color 0.3s ease;
  }

  button:hover {
    background-color: #2980b9;
  }

  .data-section, .error-section {
    margin-top: 20px;
    padding: 20px;
    border-radius: 8px;
    background-color: #ecf0f1;
    height: 800px;
  }

  .data-section h2, .error-section h2 {
    margin: 0 0 10px;
    color: #2c3e50;
  }

  pre {
    background-color: #2c3e50;
    color: white;
    padding: 15px;
    border-radius: 6px;
    max-height: 700px;
    overflow-y: auto;
  }
  </style>
