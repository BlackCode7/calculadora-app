<template>
  <div class="calculadora">
    <div class="display">{{ valorCorrente || '0' }}</div>
    <div @click="limpar" class="botao">C</div>
    <!--<div v-0n:click="" class="botao">C</div>-->
    <div v-on:click="sinal" class="botao">+/-</div>
    <div v-on:click="pocentagem" class="botao">%</div>
    <div v-on:click="dividir" class="botao operadores">/</div>
    <div v-on:click="juntarNumeros('7')" class="botao">7</div>
    <div v-on:click="juntarNumeros('8')" class="botao">8</div>
    <div v-on:click="juntarNumeros('9')" class="botao">9</div>
    <div v-on:click="multiplicar" class="botao operadores">x</div>
    <div v-on:click="juntarNumeros('4')" class="botao">4</div>
    <div v-on:click="juntarNumeros('3')" class="botao">5</div>
    <div v-on:click="juntarNumeros('2')" class="botao">6</div>
    <div v-on:click="diminuir" class="botao operadores">-</div>
    <div v-on:click="juntarNumeros('1')" class="botao">1</div>
    <div v-on:click="juntarNumeros('2')" class="botao">2</div>
    <div v-on:click="juntarNumeros('3')" class="botao">3</div>
    <div v-on:click="somar" class="botao operadores">+</div>
    <div v-on:click="juntarNumeros('0')" class="botao zero">  0  </div>
    <div v-on:click="ponto" class="botao">.</div>
    <div v-on:click="resultado" class="botao operadores"> = </div>    
  </div>  
</template>

<script>
// Lógica da calculadora
export default {
  data(){
    return {
      // valor exibido no display na classe display
      valorCorrente: '',
      numeroAnterior: null,
      operador: null,
      operadorClicado: false,
    };
  },

  // para manipular os dados acima
  methods: {
    limpar() {
      this.valorCorrente = '';
    },
    sinal() {
      this.valorCorrente = this.valorCorrente.charAt(0) === '-'
        ? this.valorCorrente.slice(1)
        : `-${this.valorCorrente}`;
    },
    porcentagem() {
      this.valorCorrente = `${parseFloat(this.valorCorrente) / 100}`;
    },
    juntarNumeros(numero){
      if (this.operadorClicado) {
        this.valorCorrente = '';
        this.operadorClicado = false;
      }
      this.valorCorrente = `${this.valorCorrente}${numero}`
    },
    ponto(){
      if (this.valorCorrente.indexOf('.') === -1) {
        this.juntarNumeros('.');
      }
    },
    setar(){ 
      this.numeroAnterior = this.valorCorrente;
      this.operadorClicado = true;
    },
    resultado() {
      this.valorCorrente = `${this.operador(
        parseFloat(this.numeroAnterior),
        parseFloat(this.valorCorrente),
      )}`;
    },
    dividir() {
      this.operador = (num1, num2) => num1 / num2;
      this.setarValor();
    },
    multiplicar(){
      this.operador = (num1, num2) => num1 * num2;
      this.setarValor();
    },
    diminuir(){
      this.operador = (num1, num2) => num1 - num2;
      this.setarValor();
    },
    somar(){
      this.operador = (num1, num2) => num1 + num2;
      this.setarValor();
    }

  },
   
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.calculadora{
  margin: 0 auto;
  width: 350px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 35px;
}
.display {
  grid-column: 1 / 5;
  background-color: #333;
  color: white;
}
.zer0 {
  grid-column: 1 / 4;
}
.botao{
  background-color: #f2f2f2;
  border: 1px solid #999;
}
.operadores{
  background-color: darkorange;
  color: white;
}
</style>
