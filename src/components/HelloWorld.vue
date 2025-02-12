<template>

<div class="container-titulo">
    <h1><img src="@/assets/Digimon_Logo.webp" alt="Logo" style="width: 500px; height: 200px;"></h1>
</div>


<label >HOLA SOY Ivan</label>

<label >HOLA SOY Linea Ivan</label>

  <div class="container">
    <!-- Contenedor de tarjetas con Grid -->
    <div class="card-container">
      <div v-for="digimon in digimones.content" :key="digimon.name" class="card">
        <img :src="digimon.image" alt="Imagen de Digimon">
        <h2><img src="@/assets/digivice.webp" alt="Logo" style="width: 20px; height: 20px;"> {{ digimon.name }}</h2>
        <!-- <h2><img src="@/assets/fuego.png" alt="Logo" style="width: 20px; height: 20px;">{{ digimon.content.level }}</h2>-->
      </div>

    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const digimones = ref([])
const pageSize = 50;
//https://digi-api.com/api/v1/digimon?pageSize=${pageSize};

// Cargar los datos cuando el componente se monta
onMounted(() => {
  fetch(`https://digi-api.com/api/v1/digimon?pageSize=${pageSize}`)
    .then(response => response.json())
    .then(data => {
      console.log(data)
      digimones.value = data
    })
})
</script>

<style>
/* Estilos generales */

body {
  /*background-color: #f5be0af3;*/
  background: linear-gradient(to right, #e4b61fda, #f07e14);
  font-family: Arial, sans-serif;
  text-align: center;
}

.container-titulo {
  /*max-width: 1200px;*/
  margin: 10px auto;
  /*padding: 20px 40px; /* 20px arriba/abajo, 40px izquierda/derecha */
  box-sizing: border-box; /* Evita que el padding afecte el tamaño */
}

/* Contenedor principal */
.container {
  border-radius: 10px;
  max-width: 1200px;
  margin: 20px auto;
  padding: 20px 40px; /* 20px arriba/abajo, 40px izquierda/derecha */
  box-sizing: border-box; /* Evita que el padding afecte el tamaño */
  background:  #0f3175
}


/* Estilos para el título */
h1 {
  font-size: 2rem;
  margin-bottom: 10px;
  color: #333;
}

h4 {
  color: #f00c0c;
  margin-bottom: 20px;
}

/* Contenedor de tarjetas con Grid */
.card-container {
  border-radius: 10px;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr)); /* Mínimo 200px por tarjeta */
  gap: 20px;
  justify-content: center;
  max-width: 1100px; /* Ajuste al ancho máximo */
  margin: auto; /* Centrar el contenedor */
}

/* Tarjeta individual */
.card {
  border-radius: 10px;
  background-color: rgb(255, 255, 255);
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  padding: 15px;
  text-align: center;
  transition: transform 0.2s ease-in-out;
}

.card:hover {
  transform: scale(1.05);
}

/* Imagen dentro de la tarjeta */
.card img {
  width: 100%;
  height: 150px;
  object-fit: contain;
  border-radius: 10px;
}

/* Nombre del Digimon */
.card h2 {
  font-size: 1.2rem;
  color: #333;
  margin-top: 10px;
}
</style>
