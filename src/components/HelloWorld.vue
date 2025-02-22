<template>

<div class="container-titulo">
    <h1><img src="@/assets/Digimon_Logo.webp" alt="Logo" style="width: 500px; height: 200px;"></h1>
</div>

<button @click="toogglePage">Siguiente pagina</button>

  <div class="container">
    <!-- Contenedor de tarjetas con Grid -->
    <div class="card-container">
      <div v-for="digimon in digimones.content" :key="digimon.name" class="card">

        <div @click="showDigimon(digimon.id)">
          <img :src="digimon.image" alt="Imagen de Digimon">
          <h2><img src="@/assets/digivice.webp" alt="Logo" style="width: 20px; height: 20px;"> {{ digimon.name }}</h2>
        </div>

      </div>

    </div>
  </div>

  <ModalComponent :tooggleModalHijo="tooggleModalPapa" :oneDigimonInfo="digimonDetail" @closeModal="fnEjemplo" @otroEmit="fnEjemplo2" />

</template>















<script setup>
import { ref, onMounted } from 'vue'
import ModalComponent from './ModalComponent.vue'

const digimones = ref([])
const digimonDetail = ref({})
const pageSize = ref(20)
const page = ref(0)
const tooggleModalPapa = ref(false)
const totalPagesDigimon = ref(0)  

const nameDigimonSearch = ref('')

// Cargar los datos cuando el componente se monta
onMounted(() => {
  callDigiApiAllDigimons()
});

const togglePage = (increment) => {
  if (increment) {
    page.value == totalPagesDigimon.value ? page.value = page.value : page.value += 1;
  } else {
    page.value > 0 ? page.value -= 1 : page.value = page.value ; 
  }
  callDigiApiAllDigimons();
};

const choosePag = (numPage) => {
  page.value = numPage;
  callDigiApiAllDigimons();
};

const fnEjemplo = () => {
  tooggleModalPapa.value = false
}

const fnEjemplo2 = () => {
  console.log('Funcion de ejemplo 2')
}



// Ejemplo de funcion asyncrona
const callDigiApiAllDigimons = async () => {
  const response = await fetch(`https://digi-api.com/api/v1/digimon?pageSize=${pageSize.value}&page=${page.value}`)
  const data = await response.json()

  digimones.value = data
}


const callDigiApiOneDigimonDetail = async (id) => {
  const response = await fetch(`https://digi-api.com/api/v1/digimon/${id}`)
  const data = await response.json()

  digimonDetail.value = data
}

const callDigiApiOneDigimonDetailByName = async (name) => {
  const response = await fetch(`https://digi-api.com/api/v1/digimon/${name}`)
  const data = await response.json()

  digimonDetail.value = data
  tooggleModalPapa.value = true
}

const showDigimon = (id) => {
  tooggleModalPapa.value = true
  callDigiApiOneDigimonDetail(id)
}
 
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


.modal-container {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  color: #333;
  display: flex;
  justify-content: center;
  align-items: center;
}

.modal {
  background-color: #fff;
  border-radius: 10px;
  padding: 20px;
  color: #333;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  width: 100%;
}

</style>
