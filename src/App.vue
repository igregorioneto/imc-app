<template>
  <div>
    <div>
      <h1>Cálculo do IMC</h1>
      <h2>Digite seu peso e altura para calcular o IMC</h2>

      <span class="p-float-label">
        <InputText id="input-peso" type="text" v-model="peso"/>
        <label for="input-peso">Peso</label>
      </span>  

      <span class="p-float-label">
        <InputText id="input-altura" type="text" v-model="altura"/>
        <label for="input-altura">Altura</label>
      </span>
    </div>      

      <div class="button">
        <span v-if="!resultado">
          <span>
            <Button label="CALCULAR" @click="calculoIMC"/>
          </span>
          <span class="button-limpar">
            <Button label="LIMPAR" @click="limparCampos"/>
          </span> 
        </span>                  
      </div>

      <div class="resultado-calculo">
        <span v-if="resultado">
          <p class="font">IMC: {{resultado}}</p>
          <p>Seu tipo é: {{tipoImc}}</p>
        </span>        
      </div>

      <div>
        <span v-if="resultado">
          <Button label="NOVO CÁLCULO" @click="novoCalculo"/>
        </span>
      </div>
      
  </div>
</template>

<script>


export default {
  data(){
    return{
      peso: null,
      altura: null,
      resultado: null,
      tipoImc: ""
    }
  },
  methods:{
    calculoIMC:function(){
      const imc = (this.peso / (this.altura * this.altura)).toFixed(2);
      this.resultado = imc;
      if(imc < 18.5){
        this.tipoImc = "Magreza";
      }else if(imc >= 18.5 && imc < 25){
        this.tipoImc = "Normal";
      }else if(imc >= 25 && imc < 30){
        this.tipoImc = "Sobrepeso";
      }else if(imc >= 30 && imc < 40){
        this.tipoImc = "Obesidade";
      }else{
        this.tipoImc = "Obesidade Grave";
      }
    },
    limparCampos(){
      this.peso = null;
      this.altura = null;
    },
    novoCalculo(){
      this.resultado = false;
      this.peso = null;
      this.altura = null;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}

.p-float-label{
  margin-top: 1.2rem;
}

.button{
  margin-top: 0.9rem;
}

.button-limpar{
  padding: 0.5rem !important;
}

.font{
  font-size: 1.2rem;
}
</style>
