<template>

<!-- Contenedor de tarjetas con Grid -->
<div class="card-container">
    <div v-for="digimon in oneDigimonInfo.content" :key="digimon.name" class="card">

        <div @click="showDigimon(digimon.id)">
          <img :src="digimon.image" alt="Imagen de Digimon">
          <h2><img src="@/assets/digivice.webp" alt="Logo" style="width: 20px; height: 20px;"> {{ digimon.name }}</h2>
        </div>

    </div>
</div>

</template>

<script setup>

// Importar las props
import { defineProps } from 'vue';

const props = defineProps({
  oneDigimonInfo: Object
});


</script>