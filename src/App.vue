<script setup>
import { reactive, watch } from 'vue';

const estado = reactive({
    filtro: 'adicao',
    numero1: 0,
    numero2: 0, 
    resultado: 0,
});

const calcular = () => {
    const num1 = parseFloat(estado.numero1);
    const num2 = parseFloat(estado.numero2);

    
    if (isNaN(num1) || isNaN(num2)) {
        estado.resultado = 'Por favor, insira números válidos';
        return;
    }

    switch (estado.filtro) {
        case 'adicao':
            estado.resultado = num1 + num2;
            break;
        case 'subtracao':
            estado.resultado = num1 - num2;
            break;
        case 'multiplicacao':
            estado.resultado = num1 * num2;
            break;
        case 'divisao':
            if (num2 !== 0) {
                estado.resultado = num1 / num2;
            } else {
                estado.resultado = 'Divisão por zero não é definida';
            }
            break;
        default:
            estado.resultado = 'Operação inválida';
    }
};

watch([() => estado.numero1, () => estado.numero2, () => estado.filtro], () => {
    calcular();
}, { immediate: true });
</script>

<template>
    <header class="cabecalho">
        <h1 class="titulo">Calculadora Aritmética</h1>
    </header>
    <div class="container">
        <div class="calculos">
            <select v-model="estado.filtro" class="item">
                <option value="adicao">Adição</option>
                <option value="subtracao">Subtração</option>
                <option value="multiplicacao">Multiplicação</option>
                <option value="divisao">Divisão</option>
            </select>
            <input v-model.number="estado.numero1" class="item" type="number" required />
            <input v-model.number="estado.numero2" class="item" type="number" required />
        </div>
    </div>
    <div class="container">
        <p class="resultado">Resultado: {{ estado.resultado }}</p>
    </div>
</template>

<style scoped>
* {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    font-family: sans-serif;
}

.cabecalho {
    display: flex;
    justify-content: center;
    background-color: rgb(58, 57, 57);
    padding: 40px;
    max-width: 800px;
    margin: 0 auto;
}

.container {
    display: flex;
    max-width: 800px;
    width: 100%;
    justify-content: center;
    margin: 0 auto;
    background-color: #ccc;
}

.calculos {
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 70px;
}

.titulo {
    color: #fff;
}

.item {
    margin-right: 6px;
    padding: 12px 6px;
}

.btn-calcular {
    margin-right: 6px;
    padding: 12px 6px;
    background-color: rgb(58, 57, 57);
    color: #fff;
}

.btn-calcular:hover {
    background-color: rgb(102, 101, 101);
    cursor: pointer;
}

.resultado {
    font-size: 32px;
    font-weight: bold;
    margin-bottom: 32px;
}
</style>