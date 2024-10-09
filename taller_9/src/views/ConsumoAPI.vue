<template>
    <section>
      <header>
        <h1>API Data Fetcher</h1>
      </header>

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
