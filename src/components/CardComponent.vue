<template>

        <div @click="showDigimon()">
          <img :src="oneDigimonInfo.image" alt="Imagen de Digimon">
          <h2><img src="@/assets/digivice.webp" alt="Logo" style="width: 20px; height: 20px;"> {{ oneDigimonInfo.name }}</h2>
        </div>

</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  oneDigimonInfo: Object
});

const emits = defineEmits(['showDigimonEmit']);

const showDigimon = () => {
  emits('showDigimonEmit');
}

</script>