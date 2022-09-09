<script setup>
    import { RouterView } from 'vue-router'
</script>

<template>
    <div id="root">
        <img alt="925-logo" class="logo" src="@/assets/925.png" width="125" height="125" />
        <div class="router-view"><RouterView /></div>
    </div>
</template>

<style lang="less" scoped>
    #root {
        height: 100%;
        display: flex;
        flex-direction: column;
        .logo {
            align-self: center;
            margin: 2em;
        }
        .router-view {
            flex: 1;
        }
    }
</style>

<style>
    @font-face{
        font-family: 'pixel';
        src: url('@/assets/pixel.woff2');
    }
    html, body {
        margin: 0;
        padding: 0;
        border: none;
        height: 100%;
        width: 100%;
    }
    body > #app {
        height: 100%;
        background-color: #181818;;
    }
    * {
        box-sizing: border-box;
        color: rgba(235, 235, 235, 0.64);
    }
</style>