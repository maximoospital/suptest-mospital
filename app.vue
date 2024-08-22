<template>
  <div>
      <h1>ID Validator</h1>
      <input type="name" placeholder="nombre" v-model="nombre"/>
      <input type="name" placeholder="apellido" v-model="apellido" />
      <input type="name" placeholder="ID" v-model="id" />
      <button @click="verify()">Validar</button>
      <p v-if="verified">{{ this.valid }}</p>
      <p v-if="verified">Nombre: {{ this.nombre }} Apellido: {{ this.apellido }} ID: {{ this.new_id }}</p >
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
              console.log("Nombre: " + this.nombre + " Apellido: " + this.apellido + " ID: " + this.id);
              // id_sourcenumber should start after the 4th character and end before the - character
              const numericPart = this.id.replace(/\D/g, ''); // Remove non-numeric characters
              const id_sourcenumber = numericPart.slice(0, -1); // Remove the last digit
              console.log("ID Source Number: " + id_sourcenumber);
              let new_id = this.apellido.toUpperCase().slice(0, 2) + this.nombre.toUpperCase().slice(0, 2) + id_sourcenumber + '-' + this.createVerificationDigit(id_sourcenumber);
              console.log("New ID: " + new_id);
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
            let oddPosition = [];
            let evenPosition = [];
            let digits = [];
            for (let i = 0; i < numLength; i++) {
              let digit = parseInt(number[i]);
              S += digit;
              digits.push(digit);
              if (i % 2 === 0) {
                O += digit;
                oddPosition.push(digit);
              } else {
                E += digit;
                evenPosition.push(digit);
              }
            }
            console.log("Digits: " + digits);
            console.log("Odd Position Digits: " + oddPosition);
            console.log("Even Position Digits: " + evenPosition);
            console.log("S: " + S + " O: " + O + " E: " + E);
            let X = (O * 2) + (E * 3) + S;
            console.log("X: " + X);
            let verificationDigit = X % 10;
            console.log("Y / Verification Digit: " + verificationDigit);

            return verificationDigit;
          }
      }
  }
</script>
