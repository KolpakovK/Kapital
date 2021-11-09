<template>
    <a v-bind:href="url" class="decoration-none result-card">
        <p class="decoration-none text-white text-light opacity7">{{title}}</p>
        <p class="decoration-none text-white text-bold">{{cost + ' грн.'}}</p>
    </a>
</template>

<script>
    export default{
        name: 'ResultCard',
        props:{
            title: String,
            url:String,
            cost: String,
        },
    }
</script>

<style>
    .result-card{
        padding: 16px;
        box-sizing: border-box;
        display: flex;
        justify-content: space-between;
        align-items: center;
        background: #22222C;
        border-radius: 8px;
        margin-bottom: 8px;
    }

    
</style>