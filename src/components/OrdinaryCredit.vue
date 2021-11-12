<template>
    <div class="form">
        <h1>Калькулятор</h1>
        <div class="form__main">
            <InputText ref="amount" label="Сумма" name="input_sum" />
            <InputText ref="term" label="Срок(в мес)" name="input_term" />
            <InputText ref="rate" label="Ставка" name="input_rate" />
            <div class="form__main__block-buttons">
                <button @click="reset()">Сбросить</button>
                <button @click="considerCredit()" >Рассчитать</button>
            </div>           
        </div>
        <div v-if="result_consider && monthly_payment" class="form__result">
            <h3>Платеж в месяц: {{ monthly_payment }}</h3>
            <h3>Итоговая сумма: {{ result_consider }}</h3>
        </div>
    </div>
</template>

<script>

import InputText from '@/components/helpers/InputText.vue'

export default {
    name: 'OrdinaryCredit',
    components: {
        InputText
    },
    data() {
        return {
            result_consider: null,
            monthly_payment: null
        }
    },
    methods: {
        displayMoney(x){
            return parseInt(x * 100) / 100
        },
        validationDate(amount, term, rate){
            if (amount && term && rate)
                return true
            return false
        },
        considerCredit(){
            const amount = this.$refs.amount.value
            const term = this.$refs.term.value
            const rate = this.$refs.rate.value / 12
            const error = this.validationDate(amount, term, rate)
            if (!error){
                alert("Заполните поля")
            }
            else{
                const tmp = Math.pow((1 + rate), term)
                const res = amount * rate * tmp / (tmp - 1) // (1 + rate)^term
                this.result_consider = this.displayMoney(res * term)
                this.monthly_payment = this.displayMoney(res)
            }
        },
        reset(){
            this.monthly_payment = null
            this.result_consider = null
            this.$refs.amount.value = ""
            this.$refs.term.value = ""
            this.$refs.rate.value = ""
        }
    }
}
</script>

<style scoped lang="scss">
    .form{
        width: 1200px;
        margin: 0 auto;
        border: 1px solid #2c3e50;
        padding: 15px;
        @media screen and (max-width:1280px){
            width: 600px;
            h1{
                font-size: 28px !important;
            }
        }
        @media screen and (max-width:640px){
            width: 320px;
            padding: 5px;
            h1{
                font-size: 24px !important;
            }
        }
        h1{
            text-align: center;
            color: #2c3e50;
            font-size: 36px;
            font-weight: bold;
        }
        &__main, &__result{
            margin-top: 32px;
            border-top: 1px solid #2c3e50;
            h3{
                color: #2c3e50;
                font-size: 24px;
            }
            &__block-buttons{
                display: flex;
                justify-content: space-around;
                margin-top: 32px;
                button{
                    font-size: 18px;
                    padding: 10px 15px;
                    cursor: pointer;
                    display: flex;
                    background-color: white;
                    transition-duration: .3s;
                    border: 1px solid rgb(73, 73, 243);
                    &:hover{
                        background-color: rgb(73, 73, 243);
                        color: white;
                    }
                }
            }
            
        }
    }
</style>
