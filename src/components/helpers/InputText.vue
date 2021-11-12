<template>
    <div class="input-block">
        <label :for="name"> 
            {{label}}: 
        </label>
        <input 
            :name="name" 
            :id="name" 
            type="text" 
            placeholder="Введите значение"
            v-model="value"
        >
    </div>
</template>

<script>    
export default {
    name: 'InputText',
    props:{
        label: String,
        name: String
    },
    data() {
        return {
            value:""
        }
    },
}
</script>

<style scoped lang="scss">
    .input-block{
        margin-top: 15px;
        width: 100%;
        display: flex;
        justify-content: space-between;
        align-items: center;
        label{
            font-size: 18px;
            color: black;
            cursor: pointer;
        }
        input{
            padding: 10px 15px;
            width: 75%;
            font-size: 18px;
            color: black;
            outline: none;
            border: 1px solid #C6C6C6;
            transition-duration: .3s;
            &:focus-visible{
                box-shadow: rgba(73, 73, 243, 0.986) 0px 0px 10px 0 inset;
            }
        }
    }
</style>
