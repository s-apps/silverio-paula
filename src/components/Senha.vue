<template>
    <div class="question-title">Questão 1</div>
    <div class="question-title">Processamento de senha:</div>
    <div class="question-text">
        Crie funções de conferência para cada elemento necessário à entrada de senha
        (ao menos um caractere minúsculo, ao menos 8 caracteres, senhas iguais, etc...)
        e exiba os pontos conferidos apenas quando o usuário começar a digitar na caixa
        de texto.
    </div>

    <div class="form-group">
        <label for="senha"> <span> Senha: </span> </label>
        <input v-model="senha" type="password" id="senha" placeholder="Insira sua senha..." required v-on:keyup="validar"/>

        <label for="senha"> <span> Repita a senha: </span> </label>
        <input v-model="senhaConf" type="password" id="senhaConf" placeholder="Repita a senha..." required v-on:keyup="senhasCorrespondem"/>
    </div>

    <span v-if="!passwordMatch" class="senha-err">As duas senhas devem ser iguais!</span>

    <span v-if="erro" class="senha-err">
        <ul>
            <li :class="{'conferido': peloMenosUmCaracterMinusculo}">Pelo menos um caractere minúsculo</li>
            <li :class="{'conferido': peloMenosUmCaractereMaiusculo}">Pelo menos um caractere maiúsculo</li>
            <li :class="{'conferido': peloMenosUmCaracterEspecial}">Pelo menos um caractere especial</li>
            <li :class="{'conferido': peloMenosUmCaractereNumerico}">Pelo menos um caractere numérico</li>
            <li :class="{'conferido': peloMenosOitoCaracteres}">Pelo menos oito caracteres</li>
        </ul>
    </span>
</template>

<script>
    export default {
        name: "Senha",
        data() {
            return {
                senha: "",
                senhaConf: "",
                peloMenosUmCaractereNumerico: false,
                peloMenosOitoCaracteres: false,
                peloMenosUmCaracterEspecial: false,
                peloMenosUmCaractereMaiusculo: false,
                peloMenosUmCaracterMinusculo: false,
                passwordMatch: true
            };
        },
        computed: {
            erro() {
                if (this.senha.length > 0){
                    return true;
                }
                return false;
            }
        },
        methods: {
            validar(){
                if (this.temPeloMenosOitoCaracteres()) {
                    this.peloMenosOitoCaracteres = true;
                } else {
                    this.peloMenosOitoCaracteres = false;
                }

                if (this.temPeloMenosUmCaractereNumerico()) {
                    this.peloMenosUmCaractereNumerico = true;
                } else {
                    this.peloMenosUmCaractereNumerico = false;
                }

                if (this.temPeloMenosUmCaracterEspecial()) {
                    this.peloMenosUmCaracterEspecial = true;
                } else {
                    this.peloMenosUmCaracterEspecial = false;
                }

                if (this.temPeloMenosUmCaractereMaiusculo()) {
                    this.peloMenosUmCaractereMaiusculo = true;
                } else {
                    this.peloMenosUmCaractereMaiusculo = false;
                }

                if (this.temPeloMenosUmCaracterMinusculo()) {
                    this.peloMenosUmCaracterMinusculo = true;
                } else {
                    this.peloMenosUmCaracterMinusculo = false;
                }
            },
            temPeloMenosOitoCaracteres(){
                return this.senha.length >= 8;
            },
            temPeloMenosUmCaractereNumerico(){
                return this.senha.match(/[0-9]/gi);  
            },
            temPeloMenosUmCaracterEspecial(){
                return this.senha.match(/[*@!#%&()^~{}]+/gi); 
            },
            temPeloMenosUmCaractereMaiusculo(){
                return this.senha.match(/^.*[A-Z].*$/); 
            },
            temPeloMenosUmCaracterMinusculo(){
                return this.senha.match(/^.*[a-z].*$/);
            },
            senhasCorrespondem(){
                this.passwordMatch = this.senha == this.senhaConf;
            }
        }
    }
</script>

<style scoped>
 .form-group {
     display: grid;
     margin: 0 auto;
     grid-template-columns: auto 1fr;
     grid-template-rows: auto;
     grid-column-gap: 20px;
     grid-row-gap: 5px;
     width: 80%;
     margin-bottom: 5px;
 }

 @media query screen and (max-width: 800px) {
     .form-group {
         width: calc(100% - 20px);
     }
 }

 .form-group > label {
     display: flex;
     justify-content: center;
     align-content: center;
     flex-direction: column;
 }

 .form-group > label > span {
     width: 100%;
 }

 .form-group > input {
     border: 1px solid grey;
     border-radius: 5px;
 }

 .conferido {
     color: green !important;
 }

 .senha-err {
     color: red;
 }
</style>
