<template>
    <div class="modal-container" v-if="stateModal">
        <div class="modal">
            <h4>Modal</h4>

            <img :src="digimonDetail.images[0].href"  alt="Imagen de Digimon"><br>

            <div class="modal-info-left modal-text">
            <label class="sub-text">Nombre:</label><label> {{ digimonDetail.name }} </label><br>
            <!-- <label class="sub-text">Nivel: </label><label>{{ digimonDetail.levels.length > 0 ? digimonDetail.levels[0].level : 'N/A' }} </label><br> -->

            <label class="sub-text">Nivel: </label>

            <div v-for="digimonOne in digimonDetail.levels">
                <label>{{digimonOne.level }} </label>
            </div>

            <!-- <label>{{digimonDetail.levels.length == 0 ? 'N/A' : '' }} </label> <br>  -->

            <div v-if="digimonDetail.levels.length == 0">
                'N/A'
            </div>


            <label class="sub-text">Tipo: </label><label>{{ digimonDetail.types[0].type }} </label>
            </div>

            <div class="modal-info-right modal-text">
            <label class="sub-text">Skills:</label>
            <div v-for="digimonOne in digimonDetail.skills">
                <label style="font-family: sans-serif;"> <ul><li>{{digimonOne.skill }} </li></ul></label>
                </div>

            </div>
            <div class="modal-info-under">
                <button class="styled-button" @click="closeModal">Cerrar</button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps({
    digimonDetail: Object,
    stateModal: Boolean
})

const emits = defineEmits(['closeModal'])

const closeModal = () => {
    emits('closeModal');
}

</script>

<style lang="scss" scoped>

</style>