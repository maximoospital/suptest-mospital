<template>
  <div>
      <h1>ID Validator</h1>
      <input type="name" placeholder="nombre" v-model="nombre"></input> 
      <input type="name" placeholder="apellido" v-model="apellido"></input> 
      <input type="name" placeholder="ID" v-model="id"></input> 
      <button @click="verify()">Validar</button>
      <p v-if="verified">{{ this.valid }}</p>
  </div>
</template>
<script>
  export default {
      data() {
          return {
              nombre: '',
              apellido: '',
              id: '',
              valid: false,
              verified: false
          }
      },
      methods: {
          verify() {
              this.verified = true;
              console.log("Nombre: " + this.nombre + " Apellido: " + this.apellido + " ID: " + this.id);
              let id_vn = Number(this.id.slice(13, 14));
              let id_sourcenumber = this.id.slice(4, 12);
              let id_sourcenumber_sum = id_sourcenumber.toString().split('').map(Number).reduce(function (a, b){ return a + b; }, 0);
              let id_sourcenumber_sum_even = this.sumEven(id_sourcenumber);
              let id_sourcenumber_sum_odd = this.sumOdd(id_sourcenumber);
              let X = 3* id_sourcenumber_sum_even + 2*id_sourcenumber_sum_odd + id_sourcenumber_sum;
              let new_id_vd = X % 10;
              let new_id = this.apellido.toUpperCase().slice(0, 2) + this.nombre.toUpperCase().slice(0, 2) + id_sourcenumber + '-' + new_id_vd;
              console.log("ID: " + new_id);
              if(new_id === this.id){
                  this.valid = "OK";
              } else {
                  this.valid = "NOT VALID";
              }
          },
          sumEven(number){
              let sumNumber = 0;
              let numLength = number.length;
              for (let i = 0; i < numLength; i++) {
                  if (i % 2 != 0) {
                      sumNumber += parseInt(number[i]);
                  }
              }
              return sumNumber;
          },
          sumOdd(number){
              let sumNumber = 0;
              let numLength = number.length;
              for (let i = 0; i < numLength; i++) {
                  if (i % 2 === 0) {
                      sumNumber += parseInt(number[i]);
                  }
              }
              return sumNumber;
          }
      },
      mounted() {
          console.log("Test");
      }
  }
</script>
<style>
</style>