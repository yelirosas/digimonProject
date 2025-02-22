<template>

<div class="modal-container" v-if="tooggleModalHijo">
    <div class="modal">
      <h4>Modal Hijo</h4>

      <img :src="oneDigimonInfo.images[0].href" alt="Imagen de Digimon" /><br />

      <div class="modal-info-left modal-text">
        <label class="sub-text">Nombre:</label
        ><label> {{ oneDigimonInfo.name }} </label><br />

        <label class="sub-text">Nivel: </label>

        <div v-for="digimonOne in oneDigimonInfo.levels">
          <label>{{ digimonOne.level }} </label>
        </div>

        <!-- <label>{{digimonDetail.levels.length == 0 ? 'N/A' : '' }} </label> <br>  -->

        <div v-if="oneDigimonInfo.levels.length == 0">'N/A'</div>

        <label class="sub-text">Tipo: </label
        ><label>{{ oneDigimonInfo.types[0].type }} </label>
      </div>

      <div class="modal-info-right modal-text">
        <label class="sub-text">Skills:</label>
        <div v-for="digimonOne in oneDigimonInfo.skills">
          <label style="font-family: sans-serif">
            <ul>
              <li>{{ digimonOne.skill }}</li>
            </ul></label
          >
        </div>
      </div>
      <div class="modal-info-under">
        <button class="styled-button" @click="closeModal">
          Cerrar
        </button>
      </div>
    </div>
  </div>

</template>

<script setup>
// Importar las props
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  tooggleModalHijo: Boolean,
  oneDigimonInfo: Object
});

const emits = defineEmits(['closeModal', 'otroEmit']);

const closeModal = () => {
  emits('closeModal');
  emits('otroEmit');
};

</script>

<style lang="scss" scoped></style>
