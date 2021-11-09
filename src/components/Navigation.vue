<template>
    <div id="Navigation">
        <h2 class="text-bold text-white">KAPITAL</h2>

        <nav>
            <a href="" class="decoration-none text-regular text-white">Вопросы-ответы</a>
            <a href="" class="decoration-none text-medium text-white button">Онлайн оценка</a>
        </nav>
    </div>
</template>

<script>
    export default{
        name: 'Navigation',
    }
</script>

<style>
    #Navigation{
        margin-top: 24px;
        display: flex;
        justify-content: space-between;
        align-items: center;
    }

    #Navigation nav{
        display: flex;
        align-items: center;
        margin: 0 -12px;
    }

    #Navigation nav *{
        margin: 0 12px;
    }
</style>