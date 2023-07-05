<script setup>
    import {ref, computed} from 'vue'

    const counter = ref(0);

    const arrayNumbers = ref([]);

    const increment = () => counter.value++;

    const decrement = () => counter.value--;

    const reset = () => {
        counter.value = 0;
        arrayNumbers.value = [];
        validator.value = false;
    };

    const validator = ref(false);

    const getColorStyle = computed(() => {
        
        validator.value = arrayNumbers.value.includes(counter.value) ? true : false;

        if (counter.value < 0) {
            return { color: 'red' }
        } else if (counter.value > 0) {
            return { color: 'green' }
        } else {
            return {}
        }
    });

    const arrayInsert = () => {    
        arrayNumbers.value.push(counter.value);
    };


</script>

<template>
    <div class="counter">
        <p>
            <span :style="getColorStyle">{{ counter }}</span>
        </p>
        <br>
        <div>
            <button v-on:click="increment" class="btn btn-success">Incrementar</button>
            <button @click="decrement" class="btn btn-danger">Decrementar</button>
            <button @click="reset" class="btn btn-warning">Resetear</button>
            <button @click="arrayInsert" :disabled="validator" class="btn btn-info">Añadir</button>
        </div>
        
    </div>
    <div class="array">
        <h2>Números Favoritos</h2>
        <ul>
            <li v-for="(number, index) in arrayNumbers" :key="index">
                {{ number }}
            </li>
        </ul>
    </div>
    
</template>

<style>
    *{
        box-sizing: border-box;
        padding: 0;
        margin: 0;
    }
    html{
        font-size: 62.5%;
    }
    #app{
        display: flex;
        flex-direction: column;
    }
    .counter{
        margin: 10rem;
        display: flex;
        flex-direction: column;
        align-items: center;
    }
    p{
        font-size: 10rem;
        color: black;
    }
    .array{
        text-align: center;
    }
    .array h2{
        font-size: 6rem;
        margin-bottom: 3rem;
        color: purple;
    }
    .array li{
        font-size: 4rem;
    }
</style>