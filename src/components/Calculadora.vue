<script setup>
const props = defineProps(['elementoInclude','calcularValor', 'resultado', 'calcular', 'calcularElementos']);
</script>
<template>
    <div class="container tela">
        <header class="mb-4 mt-4">
            <h1>Calculadora</h1>
        </header>
        <!-- valores -->
        <div class="w-full rounded m-1 p-3 text-end lead fw-bold  bg-vue-pink">
            {{ props.calcularValor || 0 }} <br>
            <!-- resultado  -->
            {{ `${props.resultado}` || '' }}
        </div>
        <!-- Botões para Calcular -->
        <div class="row d-flex flex-wrap">
            <div class="col-3 py-1" v-for="(elemento, index) in props.calcularElementos" :key="index">
                <div class="lead fw-bold text-center m-1 py-3 vue-button"
                    :class="{ 'bg-vue-operator': props.elementoInclude }"
                    @click="props.calcular(elemento)">
                    {{ elemento }}
                </div>
            </div>
        </div>
    </div>
</template>

<style scoped>
.vue-button {
    background: pink;
    border-radius: 8px;
    border: 3px solid rgba(222, 150, 255, 0.74);
    outline: none;
    position: relative;
    transform-style: preserve-3d;
    transition: all 150ms cubic-bezier(.175, .885, .32, 1.275);
    box-shadow: inset 0 0 5px #707070;
}

.vue-button::before {
    background: rgb(239, 185, 255);
    border-radius: inherit;
    box-shadow:
        0 0 0 2px rgba(180, 178, 178, 0.384),
        0 .3em 0 0 rgba(194, 194, 194, 0.171);
    content: '';
    height: 100%;
    left: 0;
    position: absolute;
    top: 0;
    transform: translate3d(0, .45em, -1em);
    transition: all 150ms cubic-bezier(cubic-bezier(0.175, 0.885, 0.32, 1.275));
    width: 100%;
}

.vue-button:hover {
    cursor: pointer;
    background: rgb(251, 221, 255);
    transform: translate(0, .15em);
}

.vue-button:hover::before {
    box-shadow:
        0 0 0 2px rgb(180, 178, 178),
        0 .2em 0 0 rgba(180, 178, 178, .8);
    transform: translate3d(0, .25em, -1em);
}

.vue-button:active {
    background: rgba(255, 254, 254, 0.815);
    transform: translate(0, .45em);
}

.vue-button:active::before {
    box-shadow:
        0 0 0 3px rgb(180, 178, 178),
        0 0 rgba(180, 178, 178, .8);
    transform: translate3d(0, 0, -1em);
}

.bg-vue-pink {
    background: pink;
    border-radius: 8px;
    border: 3px solid rgb(253, 148, 218);
    outline: none;
    position: relative;
    transform-style: preserve-3d;
    transition: all 150ms cubic-bezier(.175, .885, .32, 1.275);
    box-shadow:
        0 0 0 2px rgb(180, 178, 178),
        0 .2em 0 0 rgba(180, 178, 178, .8);
    transform: translate3d(0, .25em, -1em);
}

.tela {
    max-width: 400px;
    margin: 50px auto;
    background: rgb(231, 180, 255);
    border-radius: 8px;
    border: 3px solid rgb(253, 148, 218);
    box-shadow: 0 0 25px 10px #bebdbd;

}

.bg-vue-operator {
    background: rgb(214, 248, 248);
}</style>