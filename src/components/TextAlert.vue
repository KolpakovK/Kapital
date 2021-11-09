<template>
    <!-- Блок уведомления -->
    <div class="TextAlert">
        <!-- Заголовок через параметр -->
        <h1 class="text-white text-medium">{{title}}</h1>
        <!-- Описание через параметр -->
        <p class="text-white text-light opacity7">{{description}}</p>
    </div>
</template>

<script>
    export default {
        name: "TextAlert",
        props:{
            title: String,
            description: String
        },
    }
</script>

<style>
    .TextAlert{
        padding: 32px;
        display: flex;
        flex-direction: column;
        background: radial-gradient(115.63% 1279.45% at 103.5% -6.45%, #2B3F3F 0%, rgba(43, 63, 63, 0) 100%), #23232E;
        border-radius: 32px;
    }

    .TextAlert h1{
        margin-bottom: 24px;
    }
</style>