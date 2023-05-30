<template>
    <div
            class="app">
        <div class="header">
            <h2>Решение интегралов</h2>
        </div>
        <div class="main">
            <div class="userInput appElement">
                <integral-form class="form"
                               @changeInterval="changeIntegral"
                               @changeLeft="changeLeft"
                               @changeRight="changeRight"
                               @solve="solve"
                               @reset="reset"
                               @error="error"
                />
<!--                <integral-form class="form"-->
<!--                               @error="error"-->
<!--                               @solve="solve"-->
<!--                />-->
            </div>
            <div v-if="errorMessage === ''" class="result appElement">
                <br>
                Найденное значение интеграла:
                {{ s }}
                <br><br>
                Число разбиения:
                {{ n }}
            </div>
            <div v-else class="result appElement">
                <br>
                {{ errorMessage }}
            </div>
        </div>
    </div>
</template>

<script>
import IntegralForm from "@/components/IntegralForm.vue";

export default {
    components: {
        IntegralForm,
    },
    name: "App",
    data() {
        return {
            left: -1,
            right: 1,
            eps: 0.1,
            s: '',
            n: '',
            errorMessage: '',
        };
    },
    methods: {
        changeIntegral(integral) {
            this.integral = integral
        },
        changeLeft(left) {
          this.left = left
        },
        changeRight(right) {
          this.right = right
        },
        solve(data) {
            console.log(data)
            this.s = data.s
            this.n = data.n
            this.errorMessage = ''
        },
        reset(interval, left, right) {
          this.changeIntegral(interval)
          this.changeLeft(left)
          this.changeRight(right)
        },
        error(errorMessage) {
            this.errorMessage = errorMessage;
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
    --text-size: 15px;
    --text-size-header: 40px;
    --padding-size: 5px;
    --button-size: 110px;
    --button-padding-size: 5px;
    --element-form-text-size: 15px;
}

.main {
    font-size: var(--text-size);
    display: flex;
    justify-content: space-evenly;
    margin: 20px;
    padding: 20px;
    flex-direction: row;
}

.header {
    width: 100%;
    text-align: center;
    font-size: var(--text-size-header);
    margin: 50px 0px 20px 0px;
}

.result {
    width: 400px;
    display: flex;
    flex-direction: row;
}

.appElement {

    height: 650px;
    margin: 20px;
    padding: 20px;
    border: 1.5px solid black;
    display: flex;
    flex-direction: column;
}

.userInput {
    width: 600px;
    display: flex;
    flex-direction: column;
    justify-content: space-evenly;
    --button-size: 130px;
    --button-padding-size: 10px;
    --element-form-text-size: 15px;
}
</style>

