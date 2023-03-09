<script setup>
    defineProps({
        inicio: Number,
        fin: Number,
        maxLength: Number
    });

    const activatedPrev = () => {
        console.log((inicio.value <= 0) ? 'true' : 'false')
        return (inicio.value < 0) ? 'true' : 'false'
    }
</script>

<template>
    <div class="btn-group" roles="group" aria-label="Basic Example">
        <button 
            @click="$emit('prev')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="inicio <= 0"
        >Previus {{ inicio }}</button>
        <button 
            @click="$emit('next')" 
            type="button" 
            class="btn btn-outline-primary"
            :disabled="fin == maxLength "
        >Next {{ fin }}</button>
    </div>
</template>