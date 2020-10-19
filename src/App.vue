<template>   
    <div class="main">
        <calculator></calculator>
    </div>
</template>

<script>
import Calculator from './components/Calculator.vue';
export default {
    data() {
        return {
            output: 0,
            equation: '',
        }
    },
    components: {
        Calculator,
    }
}
</script>

<style>
* {
    box-sizing: border-box;
    margin: 0;
}

body {
    margin: 0;
    padding: 0;
    height: 100vh;
    background-color: black;
    font-family: Arial, Helvetica, sans-serif;
}

.main {
    width: 30%;
    margin: auto;
    margin-top: 100px;
}
</style>
