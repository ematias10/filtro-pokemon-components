<template>
<div>
    <label>Selecciona una región: </label>
    <select v-model="regionSelecionada" @change="emitirRegion">
        <option value="2">Kanto</option>
        <option value="3">Johto</option>
        <option value="4">Hoenn</option>
        <option value="5">Sinnoh</option>

    </select>
</div>
</template>

<script setup>
import { ref } from 'vue';

const emit = defineEmits(['cambio-region']);
const regionSelecionada = ref('');

function emitirRegion(){
    emit('cambio-region', regionSelecionada.value);
}

</script>

<style scoped>
select{
    width: 200px;
    padding: 5px;
    border-radius: 5px;
    border: 1px solid #ccc;
    font-size: 16px;
}
label {
    font-size: 18px;
    margin-right: 10px;
}
</style>