<template>
    <div class="question-title">Questão 3</div>
    <div class="question-title">Edição de entradas:</div>
    <div class="question-text">
        Modifique este componente para que exiba as entradas da lista de objetos (com a estrutura abaixo) cujas as propriedades devem ser inputs no componente <tt>div.entrada</tt>, atualizando
        seus valores no componente pai caso editadas. Cada objeto na lista deve pertencer ao seu próprio elemento. Exiba todos corretamente, exiba os indicadores corretos e repasse os dados ao componente pai ao se clicar no botão atualizar.
        <br />
        <pre class="json-example"><i>// Entrada:</i>
<code>{
    id: Number,
    op1: String,
    op2: String
}</code></pre>
    </div>

    Indicadores:
    <ul>
        <li v-if="!lista">LISTA VAZIA</li>
        <li v-if="lista.length > 5">MAIS DE 5 ELEMENTOS</li>
        <li v-if="formatoInvalido">UMA OU MAIS ENTRADAS NÃO RESPEITA O FORMATO</li>
    </ul>

    <div class="entradas">
        <div class="entrada" v-for="i in lista" v-bind:key="i">
            <div class="mb">
                <label>{{ i.id }}</label>
                <input :value="i.op1" :id="i.op1">
                <input :value="i.op2" :id="i.op2">
            </div>
        </div>
    </div>

    <button type="submit" @click="update" class="form-button">Atualizar</button>
</template>

<script>
    export default {
        name: "Lista",
        props: {
            dados: {
                type: Array,
                // required: true
            }
        },
        data() {
            return {
                lista: this.dados // deve representar a lista dada
            };
        },
        watch: {},
        computed: {
            placeholder() { return true; },
            formatoInvalido(){
                for (let i = 0; i < this.lista.length; i++){
                    if(this.lista[i].id === undefined || this.lista[i].op1 === undefined || this.lista[i].op2 === undefined){
                        return true;
                    }
                }
                return false;
            }
        },
        methods: {
            update() {
                for (let i = 0; i < this.lista.length; i++){
                    let op1 = document.getElementById(this.lista[i].op1);
                    let op2 = document.getElementById(this.lista[i].op2);
                    this.lista[i].op1 = op1.value;
                    this.lista[i].op2 = op2.value;
                }
                this.$emit('mudancaEmitida', this.lista);
            }
        }
    }
</script>

<style scoped>
 .form-button {
     font-size: 1.15rem;
     border-radius: 10px;
     border: 1px solid grey;
     background-color: #2c3e50;
     display: block;
     margin: 0 auto;
     padding: 5px;
     color: whitesmoke;
     cursor: pointer;
 }

 .entradas {
     width: 100%;
 }

 .entrada {
     /* ... */
 }

 .json-example {
     font-style: normal;
     background-color: lightgrey;
     border: 1px solid #2c3e50;
     padding: 5px;
 }

 .json-example > code {
     font-family: "Courier New", monospace !important;
 }

 .mb {
     margin-bottom: 5px;
 }
</style>
