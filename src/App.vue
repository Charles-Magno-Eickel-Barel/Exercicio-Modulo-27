<script setup>
  import * as math from 'mathjs';
  import { reactive } from 'vue';
  import Calculadora from './components/Calculadora.vue';
  const estado = reactive({
    
    tarefa: [
      {
      calcularValor: '',
      ultimaString: '',
      resultado:'',
      aspas:'',
      buscarOperadores:['/', '*', '-', '+','%'],
      encontrarOperador:false,
      calcularElementos: ["C", "()", "%", "/", 7, 8, 9, "*", 4, 5, 6, "-", 1, 2, 3,"+", "<", 0, ".", "="],     
      }
    ],
  });

  function calcular(elemento)  {
  
    estado.tarefa[0].ultimaString = estado.tarefa[0].calcularValor.substring(estado.tarefa[0].calcularValor.length - 1);
      // Pegar Valores
      if(!isNaN(elemento) || elemento === '.') {
        
        if(estado.tarefa[0].ultimaString === '%'){
          estado.tarefa[0].calcularValor += "*" + '';
        }
        estado.tarefa[0].calcularValor += elemento + '';
      }
      // Apagar todos os valores 
      if(elemento === 'C') {
        estado.tarefa[0].calcularValor = '';
        estado.tarefa[0].aspas = ''
        estado.tarefa[0].resultado = ''
      }

      // Apagar os valores 
      if(elemento === '<') {
        estado.tarefa[0].calcularValor = estado.tarefa[0].calcularValor.substring(0,estado.tarefa[0].calcularValor.length -1) + ''; 
        estado.tarefa[0].ultimaString = estado.tarefa[0].calcularValor.substring(estado.tarefa[0].calcularValor.length - 1);  
        estado.tarefa[0].resultado = '';
  
      }
      
      // aspas
      if(elemento ==='()'){
        estado.tarefa[0].aspas += elemento + '';
        if(estado.tarefa[0].aspas.length === 2){
          estado.tarefa[0].calcularValor += '(' + '';
        }else{
          estado.tarefa[0].calcularValor += ')' + '';
        }
        if(estado.tarefa[0].aspas.length > 2){
          estado.tarefa[0].aspas = ''
        }
      }

      // Operações
      if(['/', '*', '-', '+','%'].includes(elemento) && estado.tarefa[0].calcularValor.length > 0) {
        estado.tarefa[0].ultimaString = estado.tarefa[0].calcularValor.substring(estado.tarefa[0].calcularValor.length - 1);
          if(['/', '*', '-', '+','%'].includes(estado.tarefa[0].ultimaString)){
            estado.tarefa[0].calcularValor = estado.tarefa[0].calcularValor.substring(0,estado.tarefa[0].calcularValor.length -1) + '';
          }
        estado.tarefa[0].calcularValor += elemento + '';
      }
    
      for (let i = 0; i < estado.tarefa[0].calcularValor.length; i++){
        if (estado.tarefa[0].buscarOperadores.includes(estado.tarefa[0].calcularValor[i])) {
          estado.tarefa[0].encontrarOperador = true;
          break;
        }
      }
      
      if(elemento === '=') {
        estado.tarefa[0].calcularValor = estado.tarefa[0].resultado + '';
      }  

      if(estado.tarefa[0].encontrarOperador) {
        estado.tarefa[0].resultado = math.evaluate(`${estado.tarefa[0].calcularValor}`);
        estado.tarefa[0].encontrarOperador = false;
      }
      if(estado.tarefa[0].calcularValor == estado.tarefa[0].resultado){
        estado.tarefa[0].resultado = '';
      }
    } 

</script>

<template>
    <Calculadora :calcularValor="estado.tarefa[0].calcularValor" 
    :resultado="estado.tarefa[0].resultado" 
    :calcularElementos="estado.tarefa[0].calcularElementos"
    :elementoInclude="['C', '*', '/', '-', '+', '%', '=', '<', '()'].includes(elemento)" 
    :calcular="calcular"
      />  
</template>


