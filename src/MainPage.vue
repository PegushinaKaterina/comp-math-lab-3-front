<template>
    <div class="app">
        <div class="header">
            <h2>Лабораторная работа №3</h2>
        </div>
        <div class="main">
            <div class="userInput">
                <my-button type="button" @click="solveIntegral()">Решить интеграл</my-button>
            </div>
        </div>
    </div>
</template>

<script>
import res from "core-js/internals/is-forced";

export default {
    name: "App",
    methods: {
        solveIntegral() {
            localStorage.token = res.data.jwtToken;
            this.$router.push({name: "integral"});
        },
    },
};
</script>

<style scoped>
*:global(*) {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    border-radius: 7px;
    background-color: #d7d4c9;
    font-family: "Courier New";
    font-weight: bolder;
    color: black;
}

.app {
    width: 100%;
    padding: var(--padding-size);
    display: flex;
    flex-direction: column;
    box-sizing: border-box;
    --text-size: 20px;
    --text-size-header: 45px;
    --padding-size: 10px;
    --button-size: 110px;
    --button-padding-size: 7px;
    --element-form-text-size: 16px;
}

.main {
    font-size: var(--text-size);
    display: flex;
    justify-content: space-evenly;
    margin-left: auto;
    margin-right: auto;
    padding: 20px;
    flex-direction: row;
    height: 300px;
}

.header {
    width: 100%;
    text-align: center;
    font-size: var(--text-size-header);
    margin: 50px 0px 20px 0px;
}

.userInput {
    width: 100%;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    --button-size: 500px;
    --button-padding-size: 15px;
    --element-form-text-size: 20px;
}
</style>
