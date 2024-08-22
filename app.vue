<template>
  <div>
      <h1>ID Validator</h1>
      <input type="name" placeholder="nombre" v-model="nombre"/>
      <input type="name" placeholder="apellido" v-model="apellido" />
      <input type="name" placeholder="ID" v-model="id" />
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
              // id_sourcenumber should start after the 4th character and end before the - character
              const start = 4;
              const end = this.id.indexOf('-');
              const id_sourcenumber = this.id.substring(start, end);
              console.log("ID Source Number: " + id_sourcenumber);
              let id_sourcenumber_sum = id_sourcenumber.toString().split('').map(Number).reduce(function (a, b){ return a + b; }, 0);
              console.log("ID Source Number Sum: " + id_sourcenumber_sum);
              let id_sourcenumber_sum_even = this.sumEven(id_sourcenumber);
              console.log("ID Source Number Sum Even: " + id_sourcenumber_sum_even);
              let id_sourcenumber_sum_odd = this.sumOdd(id_sourcenumber);
              console.log("ID Source Number Sum Odd: " + id_sourcenumber_sum_odd);
              let X = 3* id_sourcenumber_sum_even + 2*id_sourcenumber_sum_odd + id_sourcenumber_sum;
              console.log("X: " + X);
              let new_id_vd = X % 10;
              console.log("New ID VD: " + new_id_vd);
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
      }
  }
</script>
