<template>
  <div class="main">
    <div class="colored">
      <img src="@/assets/bg-main-desktop.png" alt="" />
    </div>

    <div class="cards">
        <img src="./assets/bg-card-front.png" alt="" id="front">
        <p id="card-number">{{ cardNumber }}</p>
        <p id="card-name">{{ cardName }}</p>
        <p id="card-month">{{ cardDateMonth }}/{{ cardDateYear }}</p>

        <img src="./assets/bg-card-back.png" alt="" id="back">
        <p id="cvc">{{ cvcCard }}</p>
        </div>
    <div class="white">
      <div class="">
        <form action="#">
                <label for="name">CARDHOLDER NAME</label>
                <input id="name" v-model="nameInput" type="text" class = 'wide' placeholder= "e.g. Issah Asiedu" required  />

                
                <label for="CARD NUMBER">CARD NUMBER</label>
                <input id="CARD NUMBER" v-model="numberInput" type="number" placeholder="03423423322" class="wide" @input="validateNumber();" min="0" required>
                <p v-if="showMessage" style="color: red; font-size: 12px;"> Enter up to 12 digits</p>

                <label for="exp-date">EXP. DATE(MM/YY)</label>
                <div class="exp-date">
                    <input id="exp-date" v-model="dateMonthInput" type="number" placeholder="MM" class="short" @input="validateMonth" required>
                    <input id="exp-date" v-model="dateYearInput" placeholder="YY" class="short" @input="validateYear">

                </div>
                
                <label for="CVC">CVC</label>
                <input type="number" v-model="cvcInput" placeholder="123" class="medium" @input="validateCvc()" required> 
                <p v-if="showCVCMessage" style="color: red; font-size: 12px;">Enter up to three digits</p>


                <button @click="trigger">Confirm</button>
            </form>
      </div>
    </div>
  </div>
</template>

<script setup>
import {ref} from "vue" 

//card inputs
const cardDateMonth = ref("");
const cardDateYear = ref("")
const cardName = ref("");
const cardNumber = ref("");
const cvcCard = ref("");

//form inputs
const nameInput = ref("");
const dateMonthInput = ref("");
const dateYearInput = ref("");

const numberInput = ref("");
const cvcInput = ref("")
let showMessage = ref(false)
let showCVCMessage = ref(false)

function trigger(){
    cardName.value =String(nameInput.value)
    cardNumber.value = String(numberInput.value)
    cardDateMonth.value = String(dateMonthInput.value)
    cardDateYear.value = String(dateYearInput.value)
    cvcCard.value = String(cvcInput.value)
}

    
function validateNumber() {
  numberInput.value = String(numberInput.value).slice(0, 12);

  if(numberInput.value.length < 12){
    showMessage.value = true  
} else{
    showMessage.value = false;
  }

}


function validateMonth() {
  dateMonthInput.value = String(dateMonthInput.value).slice(0, 2); 

}

function validateYear() {
  dateYearInput.value = String(dateYearInput.value).slice(0, 2); 
}

function validateCvc() {
  cvcInput.value = String(cvcInput.value).slice(0, 3); 

  if(cvcInput.value.length < 3){
    showCVCMessage = true  
} else{
    showCVCMessage = false;
  }

  
}

  

</script>

<style>


@import url("https://fonts.googleapis.com/css2?family=Fraunces:opsz,wght@9..144,400;9..144,700&family=Montserrat:wght@200;300&family=Poppins:ital,wght@1,700&family=Space+Grotesk:wght@500&display=swap");

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: "Space Grotesk", sans-serif;
}

input[type="number"]::-webkit-inner-spin-button,
input[type="number"]::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

label,
p,
input {
  font-family: "Space Grotesk", sans-serif;
}
body,
html {
  width: 100;
  height: 800px;
}

body {
  display: flex;
  justify-content: center;
  align-items: center;
}

.main {
  width: 95%;
  height: 90vh;
  display: flex;
}

.colored {
  width: 30%;
  height: 100%;
}

.colored img {
  height: 100%;
}

.white {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 66.2%;
  height: 100%;
  position: relative;
  left: 35px;
}

form {
  display: flex;
  flex-direction: column;
  gap: 10px;
  max-width: 300px;
  margin: 0 auto;
  position: relative;
  right: 100%;
}

.exp-date {
  display: flex;
  flex-direction: row;
  gap: 5px;
}

input {
  height: 30px;
  border: 1px;
  border-radius: 1px;
}

form {
  margin-top: 35%;
  margin-left: 50%;
  width: 800px;
  height: 400px;
  border: 1px;
}

input {
  border: 1px solid #e3e3e3;
  border-radius: 5px;
  width: 260px;
  margin-left: 2%;
}
label {
  font-size: 0.6em;
  font-family: sans-serif;
  color: purple;
  font-weight: 700;
  letter-spacing: 1px;
  margin-top: 5px;
}

button {
  width: 220px;
  height: 35px;
  border-radius: 4px;
  background: hsl(278, 68%, 11%);
  color: white;
  box-shadow: none;
}

.exp-date {
  display: flex;
  gap: 5px;
}

.short {
  width: 40px;
}

.medium {
  width: 60px;
}

.cards img {
  transform: scale(0.7);
}

#front {
  position: relative;
  top: 40px;
  right: 250px;
}

#back {
  position: relative;
  right: 210px;
}

#submit {
  border-radius: 5px;
}

#card-number {
  position: relative;
  bottom: 80px;
  right: 170px;
  font-size: 1.5em;
  color: white;
  letter-spacing: 3px;
}

#card-name {
  position: relative;
  bottom: 60px;
  right: 170px;
  font-size: 12px;
  color: white;
  letter-spacing: 1px;
}

#card-month {
  position: relative;
  bottom: 75px;
  left: 60px;
  font-size: 10px;
  color: white;
  letter-spacing: 3px;
}

#card-year {
  position: relative;
  bottom: 75px;
  left: 100px;
  font-size: 12px;
  color: white;
  letter-spacing: 3px;
}
#cvc {
  position: relative;
  bottom: 135px;
  left: 100px;
  font-size: 12px;
  color: white;
  letter-spacing: 3px;
}



@media all and (max-width: 600px) {

.main {
  flex-direction: column;
  width: 100vw;
  justify-content: center;
}

form {
   width: 100%;
   right: 0;
   margin-left: 0;

}

.colored{
    width: 100%;
    height: 40%;    
}

.colored img{
    width: 100%;
}
.white{
    width: 100%;
    left: 0;
}

#front{
    top: 99px;
    right: 58px;
    position: absolute;
    z-index: 1;
}

#back{
    right: 0;
}

.cards{
    position: absolute;
    display: flex;
    flex-direction: column-reverse;
    top: 30px;
    left: 15px;
}
}
</style>
