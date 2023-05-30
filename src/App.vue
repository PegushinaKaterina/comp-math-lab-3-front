<template>
    <div class="app">
        <router-view/>
    </div>
</template>

<script></script>

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
    font-size: 20px;
    width: 100%;
    padding: 10px;
    display: flex;
    flex-direction: column;
    box-sizing: border-box;
}

.main {
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
}

.form,
.graph {
    width: 25%;
}

.table {
    width: 50%;
}

.appElement {
    height: 390px;
    margin: 10px;
    padding: 20px;
    border: 1.5px solid black;
    display: flex;
    flex-direction: column;
}

.header {
    width: 100%;
    text-align: center;
    font-size: 45px;
    margin: 20px 0px 20px 0px;
}
</style>
