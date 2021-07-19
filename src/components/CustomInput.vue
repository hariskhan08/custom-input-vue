<template>
<div class="input-container popup">
  <span class="popuptext show" id="myPopup">X</span>
<button v-if="!focus" class="btn-left border-left-rounded">A</button>
  <input @focus="focus=true" @blur="focus=false" class="input-field " v-model="value" :type="type" placeholder="URL" />
  
  <button v-if="focus" class="btn-center">Y</button>
  <button class="btn-right border-right-rounded">X</button>
</div>
</template>
<script>
export default {
  name: 'CustomInput',
  props: {
    type: String,
  },
  data() {
    return {
      value: '',
      validator: false,
      focus: false,
    }
  },
}
</script>

<style scoped>

.input-container {
    
}

.btn-left{
    background-color: whitesmoke;
    padding-top: 0.2rem;
    padding-bottom: 0.2rem;
}
.btn-right{
    background-color: whitesmoke;
    padding-top: 0.2rem;
    padding-bottom: 0.2rem;
}
.btn-center{
    border: 0;
    background-color: red;
    padding-top: 0.2rem;
    padding-bottom: 0.2rem;
}

.btn-right:hover, .btn-right:focus{
    background-color: lightgray; 
    cursor: pointer;  
    transition: ease-in-out;
    transform: 0.3s;
}

.input-field{
    border:0
    }

.border-left-rounded{
    border: 0;
    border-top-left-radius: 25%;
    border-bottom-left-radius: 25%;    
}
.border-right-rounded{
    border: 0;
    border-top-right-radius: 25%;
    border-bottom-right-radius: 25%;    
}

.popup {
  position: relative;
  display: inline-block;
  cursor: pointer;
  -webkit-user-select: none;
  -moz-user-select: none;
  -ms-user-select: none;
  user-select: none;
}

/* The actual popup */
.popup .popuptext {
  visibility: hidden;
  width: 160px;
  background-color: #555;
  color: #fff;
  text-align: center;
  border-radius: 6px;
  padding: 8px 0;
  position: absolute;
  z-index: 1;
  bottom: -20%;
  left: -40%;
  margin-left: -80px;
}

/* Popup arrow */
.popup .popuptext::after {
  content: "";
  position: absolute;
  top: 40%;
  left: 103%;
  margin-left: -5px;
  border-width: 5px;
  border-style: solid;
  border-color: #555 transparent transparent transparent;
  transform: rotate(-90deg);
}

/* Toggle this class - hide and show the popup */
.popup .show {
  visibility: visible;
  -webkit-animation: fadeIn 1s;
  animation: fadeIn 1s;
}

/* Add animation (fade in the popup) */
@-webkit-keyframes fadeIn {
  from {opacity: 0;} 
  to {opacity: 1;}
}

@keyframes fadeIn {
  from {opacity: 0;}
  to {opacity:1 ;}
}
</style>