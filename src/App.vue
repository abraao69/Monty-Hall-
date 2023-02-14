<template>
    <div id="app">
        <h1>Problema de Monty Hall</h1>
        <div class="form">
            <div v-if="!started">
                <label for="portsAmount">Quantas portas?</label>
                <input type="text" id="portsAmount" size="3"
                    v-model.number="portsAmount">
            </div>
            <div v-if="!started">
                <label for="selectedPort"> Qual porta é premiada? </label>
                <input type="text" id="selectedPort" size="3"
                    v-model.number="selectedPort">
            </div>
        </div>
            <button v-if="!started" @click="started = true"> Iniciar </button>
            <button v-if="started" @click="started = false"> Reiniciar </button>
        <div class="doors" v-if="started">
            <div v-for="i in portsAmount" :key="i">
                <!-- :hasGift -> necessário para passar valor como boolean -->
                <!-- :number -> para o i ser resolvido e não passado como string  -->
                <Door :hasGift="i === selectedPort" :number="i" />
            </div>
        </div>
    </div>
</template>

<script>
import Door from './components/Door'

export default {
    name: 'App',
    components: { Door },
    data: function() { // Estado inicial
        return {
            started: false,
            portsAmount: 3,
            selectedPort: null
        }
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    font-family: 'Monteserrat', sans-serif;
    font-size: 1.2rem;
}

body {
    color: #fff;
    background: linear-gradient(to right, rgb(21, 153, 87), rgb(21, 87, 153));
}

#app {
    display: flex;
    flex-direction: column;
    align-items: center;
}

#app h1 {
    border: 1px solid #000;
    background-color: #0004;
    padding: 20px;
    margin-bottom: 40px;
}

.form {
    display: flex;
    padding: 10px;
    align-items: center;
    margin-bottom: 50px;
}

.form, .form input {
    margin-bottom: 10px;
    font-size: 1.1rem;
}

.form input {
    padding-left: 3px;
    margin-right: 20px;
    margin-left: 10px;
    border: none;
    box-shadow: 2px 2px 2px 0px #0004;
}

button {
    padding: 6px 12px;
    margin-top: 10px;
    margin-bottom: 25px;
    font-size: 1rem;
    border: none;
    box-shadow: 2px 2px 2px 0px #0004;
}

.doors {
    align-self: stretch;
    display: flex;
    justify-content: space-around;
    flex-wrap: wrap;
}

</style>