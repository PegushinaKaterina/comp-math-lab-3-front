<template>
    <form @submit.prevent>
        <div class="inputs">
            <fieldset>
                <legend>Уравнение</legend>
                <my-select v-model="integral" :options="integralOptions" @change="changeIntegral"/>
            </fieldset>
            <fieldset>
                <legend>Левая граница интервала</legend>
                <my-input v-model="left" type="number" @change="changeLeft"/>
            </fieldset>
            <fieldset>
                <legend>Правая граница интервала</legend>
                <my-input v-model="right" type="number" @change="changeRight"/>
            </fieldset>
            <fieldset>
                <legend>Погрешность вычисления</legend>
                <my-input v-model="eps" type="number"/>
            </fieldset>
            <fieldset>
                <legend>Метод вычисления</legend>
                <my-select v-model="method" :options="methodOptions"/>
            </fieldset>
                  <fieldset>
                    <legend>Файл</legend>
                    <my-input type="file" @change="changeFile"/>
                  </fieldset>
        </div>
        <div class="commandButton">
            <my-button type="button" @click="reset">Сбросить</my-button>
            <my-button type="button" @click="solve">Отправить</my-button>
        </div>
    </form>
</template>

<script>
import MyButton from "@/components/UI/MyButton.vue";
import MyInput from "@/components/UI/MyInput.vue";
import MySelect from "@/components/UI/MySelect.vue";
import axios from "axios";

export default {
    components: {MySelect, MyInput, MyButton},
    data() {
        return {
            integral: 1,
            left: -1,
            right: 1,
            x: 0,
            eps: 0.1,
            method: 1,
            file: null,
            integralOptions: [
                {value: 1, name: '4x³ - 5x² + 6x - 7'},
                {value: 2, name: "sin²(2x) / 7"},
                {value: 3, name: "-x³ - x² + x + 3"},

            ],
            methodOptions: [
                {value: 1, name: "Метод левых прямоугольников"},
                {value: 2, name: "Метод средних прямоугольников"},
                {value: 3, name: "Метод правых прямоугольников"},
                {value: 4, name: "Метод трапеций"},
                {value: 5, name: "Метод Симпсона"},
            ],
        };
    },
    methods: {
        solve() {
            if (this.eps <= 0) {
                this.$emit("error", "Погрешность вычисления должна быть больше 0");
                return;
            }
            if (this.left >= this.right) {
                this.$emit("error", "Левая граница должна быть больше чем правая");
                return;
            }
            axios
                .post(
                    "http://localhost:8081/api/integral",
                    {
                        integral: this.integral,
                        left: this.left,
                        right: this.right,
                        eps: this.eps,
                        method: this.method,
                    },
                ).then((res) => {
                this.$emit("solve", res.data);
            }).catch((error) => {
                this.$emit("error", error.response.data);
            });
        },
        reset() {
            this.integral = 1
            this.left = -1
            this.right = 1
            this.eps = 0.1
            this.method = 1
            this.file = false
            this.$emit("reset", this.integral, this.left, this.right);
        },
        changeIntegral() {
            this.$emit("changeEquation", this.integral);
        },
        changeLeft() {
            this.$emit("changeLeft", this.left);
        },
        changeRight() {
            this.$emit("changeRight", this.right);
        },
        updateValues(left, right, eps) {
          this.left = left;
          this.right = right;
          this.eps = eps;
          this.file = false;
          this.changeLeft();
          this.changeRight()
        },
        changeFile(event) {
            if (event.target.files[0].type === "text/plain") {
                let reader = new FileReader();
                reader.readAsText(event.target.files[0], 'windows-1251')
                let results;
                reader.onload = () => {
                    results = reader.result.split("\r\n");
                    if (results.length !== 3) {
                        this.file = false
                        this.$emit("error", "Неверное количество строк в файле(ожидается 3 строки).");
                    } else {
                        if (!isNaN(parseFloat(results[0])) &&
                            !isNaN(parseFloat(results[1])) &&
                            !isNaN(parseFloat(results[2]))) {

                            this.updateValues(parseFloat(results[0]), parseFloat(results[1]), parseFloat(results[2]))
                        } else {
                            this.$emit("error", "В файле ожидаются числа");
                        }
                    }
                };

                console.log(this.left)

                reader.onerror = function () {
                    this.file = false
                    this.$emit("error", "Произошла ошибка чтения из файла");
                };
            } else {
                this.file = false
                this.$emit("error", "Произошла ошибка чтения из файла");
            }

        },
    },
};
</script>

<style scoped>
fieldset {
    margin-top: 15px;
    border: 1.5px solid black;
    padding: 10px;
}

.commandButton {
    width: 100%;
    display: flex;
    flex-direction: row;
    justify-content: space-evenly;
}
</style>
