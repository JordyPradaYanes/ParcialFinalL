<script setup>
import { ref } from 'vue'
const encuesta = ref([
    {
        msj: "Entre los 14 y 18 años",
        cantidad: 0,
        color: "bg-blue-500"
    },
    {
        msj: "Entre los 19 y 25 años",
        cantidad: 0,
        color: "bg-green-500"
    },
    {
        msj: "Entre los 26 y 45 años",
        cantidad: 0,
        color: "bg-cyan-500"
    },
    {
        msj: "Mayor de 45 años",
        cantidad: 0,
        color: "bg-orange-400"
    }
]);

const rangoSeleccionado = ref(-1)
const enEncuesta = ref(true)
const sumaTotal = ref(0)


function registrarEncuesta(rango) {

    if (rango == -1) {
        alert("No has seleccionado ningún rango")
        return
    }

    const rangoEncuesta = encuesta.value[rango]
    rangoEncuesta.cantidad += 1
    sumaTotal.value += 1
    enEncuesta.value = false
}

function cambiarRangoSeleccionado(index) {
    rangoSeleccionado.value = index
}

function regresarEncuesta() {
    enEncuesta.value = true
    rangoSeleccionado.value = -1
}

</script>

<template>
    <div class="h-screen flex flex-col gap-5 justify-center items-center">
        <section v-if="enEncuesta" class="flex flex-col gap-3 max-w-3xl items-start">
            <p>¿En qué rango de edad se encuentra?</p>
            <div v-for="(rango, index) in encuesta" :key="index"
                :class="'p-2 rounded text-white w-full ' + rango.color + (rangoSeleccionado == index ? ' opacity-75' : '')"
                @click="cambiarRangoSeleccionado(index)">{{ rango.msj }}</div>

            <button @click="registrarEncuesta(rangoSeleccionado)" class="bg-red-100 p-2 rounded">Registrar</button>
        </section>

        <section class="flex flex-col gap-3 max-w-xl items-start w-full" v-else>
            <div v-for="(rango, index) in encuesta" :key="index" class="text-xl w-full flex flex-col items-start gap-2">
                <p>{{ rango.msj }}</p>
                <div :class="'p-1 rounded text-right text-white ' + rango.color"
                    :style="'width : ' + rango.cantidad / sumaTotal * 100 + '%'">
                    {{
                        Math.round(rango.cantidad / sumaTotal * 10000) / 100
                    }}%
                </div>
            </div>

            <button @click="regresarEncuesta()" class="bg-red-100 p-2 rounded">Registrar
                nuevamente</button>
        </section>
    </div>
</template>

<style></style><script setup>

</script>

<template>
    HOLA MUNDO
</template>

<style></style>