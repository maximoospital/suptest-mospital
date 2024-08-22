<template>
  <div>
      <h1>ID Validator</h1>
      <input type="name" placeholder="nombre" v-model="nombre"/>
      <input type="name" placeholder="apellido" v-model="apellido" />
      <input type="name" placeholder="ID" v-model="id" />
      <button @click="verify()">Validar</button>
      <p v-if="verified">{{ this.valid }}</p>
      <p v-if="verified">Nombre: {{ this.nombre }}</p>
      <p v-if="verified">Apellido: {{ this.apellido }}</p>
      <p v-if="verified">ID: {{ this.new_id }}</p>
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
              verified: false,
              new_id: ''
          }
      },
      methods: {
          verify() {
              this.verified = true;

              const numericPart = this.id.replace(/\D/g, '');
              const id_sourcenumber = numericPart.slice(0, -1); 

              let verificationDigit = this.createVerificationDigit(id_sourcenumber);
              let new_id = this.apellido.toUpperCase().slice(0, 2) + this.nombre.toUpperCase().slice(0, 2) + id_sourcenumber + '-' + verificationDigit;

              this.new_id = new_id;

              if(new_id === this.id){
                  this.valid = "OK";
              } else {
                  this.valid = "NOT VALID";
              }
          },
          createVerificationDigit(number) {
            let S = 0, O = 0, E = 0;
            let numLength = number.length;
            let oddPositioned = [];
            let evenPositioned = [];
            console.log("Take the numeric part of the ID without the verification digit: " + number);
            for (let i = 0; i < numLength; i++) {
              let digit = parseInt(number[i]);
              S += digit;
              if (i % 2 === 0) {
                O += digit;
                oddPositioned.push(digit);
              } else {
                E += digit;
                evenPositioned.push(digit);
              }
            }
            console.log("Sum all the numbers: " + S);
            console.log("Sum all the numbers in an odd position: " + O);
            console.log("Numbers in an odd position: " + oddPositioned);
            console.log("Sum all the numbers in an even position: " + E);
            console.log("Numbers in an even position: " + evenPositioned);
            console.log("Multiply the sum of the numbers in an odd position by 2: " + O * 2);
            console.log("Multiply the sum of the numbers in an even position by 3: " + E * 3);
            let X = (O * 2) + (E * 3) + S;
            let V = X % 10;
            console.log("Sum all the by products: " + X + " = X");
            console.log("Divide X by 10 and get the remainder: " + V);
            console.log("V is the verification digit: " + V);

            return V;
          }
      }
  }
</script>
