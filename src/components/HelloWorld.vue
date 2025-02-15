<template>

<div class="container-titulo">
    <h1><img src="@/assets/Digimon_Logo.webp" alt="Logo" style="width: 500px; height: 200px;"></h1>
</div>


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


<div class="modal-container" v-if="tooggleModal">
  <div class="modal">
    <h4>Modal</h4>

    <img :src="digimonDetail.images[0].href"  alt="Imagen de Digimon"><br>
    
    <div class="modal-info-left modal-text">
      <label class="sub-text">Nombre:</label><label> {{ digimonDetail.name }} </label><br>
      <label class="sub-text">Nivel: </label><label>{{ digimonDetail.levels[0].level }} </label><br>
      <label class="sub-text">Tipo: </label><label>{{ digimonDetail.types[0].type }} </label>
    </div>

    <div class="modal-info-right modal-text">
      <label class="sub-text">Skills:</label>
      <div v-for="digimonOne in digimonDetail.skills">
        <label style="font-family: sans-serif;"> <ul><li>{{digimonOne.skill }} </li></ul></label>
        </div>

      </div>
      <div class="modal-info-under">
        <button class="styled-button" @click="tooggleModal = false">Cerrar</button>
      </div>      
    </div>
</div>


<div class="button-container modal-info-under">
  <button class="styled-button" @click="togglePage(false)"><img src="@/assets/left.png" alt="Logo" style="width: 20px; height: 20px;">Anterior página</button>
  <button class="styled-button" @click="togglePage(true)">Siguiente página<img src="@/assets/right.png" alt="Logo" style="width: 20px; height: 20px;"></button>
</div>

<div class="container2">

</div>

</template>



<script setup>
import { ref, onMounted } from 'vue'

const digimones = ref([])
const digimonDetail = ref({})
const pageSize = ref(20)
const page = ref(0)
const tooggleModal = ref(false)

// Cargar los datos cuando el componente se monta
onMounted(() => {
  callDigiApiAllDigimons()
});

const togglePage = (increment) => {
  if (increment) {
    page.value += 1;
  } else {
    page.value -= 1;
  }
  callDigiApiAllDigimons();
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

const showDigimon = (id) => {
  tooggleModal.value = true
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

/* Contenedor principal */
.container-modal {

  background:  #f8cf1760

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
  font-size:medium;

}

.modal {
  background-color: #fff;
  border-radius: 10px;
  padding: 20px;
  color: #333;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  max-width: 600px;
  width: 100%;
  max-height: 90vh;
  overflow-y: auto;
}

    /* Contenedor para centrar los botones */
    .button-container {
      width: 100%;             /* Asegura que el contenedor ocupa el 100% del ancho */
      display: flex;
      justify-content: center; /* Centra los elementos horizontalmente */
      gap: 20px;               /* Espacio entre botones */
      margin-top: 50px;        /* Espacio superior */
    }

    /* Estilo general para los botones */
    .styled-button {
      background-color: #3498db; /* Color de fondo */
      border: none;
      border-radius: 5px;        /* Bordes redondeados */
      color: #fff;               /* Color del texto */
      padding: 10px 20px;
      font-size: 16px;
      cursor: pointer;
      transition: background-color 0.3s ease, transform 0.2s ease;
    }

    /* Efecto al pasar el cursor */
    .styled-button:hover {
      background-color: #2980b9;
      transform: translateY(-2px);
    }

    /* Efecto al hacer clic */
    .styled-button:active {
      transform: translateY(0);
    }

    .modal-info-left{
      height: auto;
      width: 230px;
      float: left;
     /* background-color: #f00c0c;*/
    }

    .modal-text{
      text-align: left;
      font-size: 110%;
      font-family: "Arial";
      line-height: 200%;
    }

    .modal-info-right{
      padding-bottom: 20px;
      height:auto;
      width: 300px;
      float: right;
     /* background-color: #2980b9;*/
    }

    .modal-info-under{
      height:80px;
      width: 100%; 
      float:inline-end;
      align-items: center;
     /* background-color: #2980b9;*/
    }

    .sub-text{
      font-weight: bold;
    }



</style>
