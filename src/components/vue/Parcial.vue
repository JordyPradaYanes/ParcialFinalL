<script setup>
import { ref } from 'vue';

const cont = ref(0);
const validar = ref(-1);
const sec = ref(true);

const rangos = ref([
    { "mesage": "Entre los 14 y 18 años", "num": 0, "color": "bg-blue-600" },
    { "mesage": "Entre los 19 y 25 años", "num": 0, "color": "bg-emerald-500" },
    { "mesage": "Entre los 26 y 45 años", "num": 0, "color": "bg-blue-400" },
    { "mesage": "Mayor a 45 años", "num": 0, "color": "bg-yellow-500" }]
);

function sumarCantidad(i) {
    if (validar.value == -1) {
        alert("No ha seleccionado")
        return
    }
    const Uno = rangos.value[i]
    Uno.num += 1
    sec.value=false
    cont.value += 1

}
function seleccionar(val) {
    validar.value = val;
}

function ingresarNuevamente() {
    sec.value = true
    validar.value = -1
}

</script>
<template>
    <div v-if="sec">
        <div class="h-screen w-1/2 m-auto">
            <div class="flex flex-col">
                <div class="mt-32 ml-2">
                    ¿En que rango de edad se encuentra?
                </div>
                <div class="h-1/2" v-for="(rec, i) in rangos" :key="i">
                    <div class="m-2 p-4 text-white rounded" :class="rec.color" @click="seleccionar(i)">

                        {{ rec.mesage }}

                    </div>
                </div>
            </div>
            <button class="bg-red-600 text-white p-3 rounded ml-2" @click="sumarCantidad(validar)">Registrar</button>
        </div>
    </div>
    <div v-else class="h-screen w-1/2 m-auto">
        <div class="flex flex-col mt-32">
            <div class="h-1/2" v-for="(rec, i) in rangos" :key="i">
                <div class="ml-2">
                    {{ rec.mesage }}
                </div>
                <div class="m-2 p-4 text-white rounded" :class="rec.color">
                    {{
                        Math.round(rec.num / cont * 100000) / 1000
                    }} %
                </div>
            </div>
        </div>
        <button class="bg-red-600 text-white p-3 rounded ml-2" @click="ingresarNuevamente()">Registrar
            nuevamente</button>
    </div>
</template>