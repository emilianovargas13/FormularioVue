<template>
    <div>
      <b-form @submit="onSubmit" @reset="onReset" v-if="show" >


        <b-form-group id="input-group-1" label="Correo Electrónico:" label-for="input-1" class="input">
          <b-form-input
            id="input-1"
            v-model="form.email"
            type="email"
            placeholder="Ingresa tu Correo Electrónico"
            required>
        
        </b-form-input>
        </b-form-group>
  
        
  
        <b-form-group id="input-group-2" label="Nombre:" label-for="input-2" class="input">

          <b-form-input
            id="input-2"
            v-model="form.name"
            placeholder="Ingresa tu Nombre"
            required>
        
        </b-form-input>
        </b-form-group>
  
  
        <b-form-group id="input-group-3" label="Apellido Paterno:" label-for="input-3" class="input">

          <b-form-input
            id="input-3"
            v-model="form.lastname"
            placeholder="Ingresa tu Apellido Paterno"
            required>

        </b-form-input>
        </b-form-group>
  
        <b-form-group id="input-group-4" label="Apellido Materno:" label-for="input-4" class="input">

          <b-form-input
            id="input-4"
            v-model="form.lastname2"
            placeholder="Ingresa tu Apellido Materno">

        </b-form-input>
        </b-form-group>
  
        <b-form-group id="input-group-5" label="Telefono:" label-for="input-5" class="input">

          <b-form-input
            id="input-5"
            v-model="form.phone"
            placeholder="Ingresa tu Numero de Telefono"
            
            :state="validatePhone()">

        </b-form-input>
        </b-form-group>
  
        <b-form-group id="input-group-6" label="Direccion:" label-for="input-6" class="input">

          <b-form-input
            id="input-6"
            v-model="form.direction"
            placeholder="Ingresa tu Direccion Completa"
            :state="validateDirection()">

        </b-form-input>
        </b-form-group>
  
        <b-form-group id="input-group-7" label="Fecha de Cumpleaños:" label-for="input-7" class="input">

          <b-form-input
            id="input-7"
            v-model="form.birthday"
            placeholder="Ingresa tu Fecha de cumpleaños (YYYY-MM-DD)"
            :state="validateBirthdate()">

        </b-form-input>
        </b-form-group>
    
        <b-form-group id="input-group-8" label="Imagen:" label-for="input-8" class="input">
          <b-form-file
            id="input-8"
            v-model="form.image"
            :state="validateImage()"
            accept=".png"
            placeholder="Selecciona una imagen PNG (máximo 5 MB)"
            :max-size="5000000">

        </b-form-file>
        </b-form-group>
        
        
  
        <b-button type="submit" variant="primary" class="btn">Submit</b-button>
        <b-button type="reset" variant="danger" class="btn">Reset</b-button>
      </b-form>
     
    </div>
  </template>
  
  
  <script>
    export default {
      data() {
        return {
          form: {
            email: '',
            name: '',
            lastname: '',
            lastname2: '',
            direction:'',
            birthday:'',
            phone:'',
            image:null
  
          },
          show: true
        }
      },
      methods: {
        onSubmit(event) {
          event.preventDefault()
          alert(JSON.stringify(this.form))
        },
  
        validateBirthdate() {
        const birthday = new Date(this.form.birthday);
        const eighteenYearsAgo = new Date();
        eighteenYearsAgo.setFullYear(eighteenYearsAgo.getFullYear() - 18);
        if (!isNaN(birthday.getTime()) && birthday < new Date() && birthday <= eighteenYearsAgo) {
          return true; 
        } else {
          return false; 
        }
      },
  
      validatePhone() {
        
        if (this.form.phone.length === 10 && /^\d+$/.test(this.form.phone)) {
          return true; 
        } else {
          return false; 
        }
      },
  
      validateImage() {
        const maxSize = 5000000; 
        if (this.form.image) {
          
          if (!this.form.image.name.toLowerCase().endsWith(".png")) {
            
            alert("Solo se permiten archivos PNG");
            return false; 
          }
  
          if (this.form.image.size > maxSize) {
            alert("La imagen excede el tamaño permitido (3 MB)");
            return false; 
          }
        }
  
        return true; 
      },
  
      validateDirection() {
        
        const directionRegex = /^(?=.*\d)(?=.*\d{5,})(?=.*\b(av|calle)?\b)(?=.*\bciudad\b).*$/i;
  
        if (directionRegex.test(this.form.direction)) {
          return true; 
        } else {
          return false; 
        }
      },
  
  
      onReset(event) {
          event.preventDefault()
          
          this.form.name = ''
          this.form.lastname = ''
          this.form.lastname2 = ''
          
          this.$nextTick(() => {
            this.show = true
          })
        }
  
    }
    }
  </script>
  
  <style>
  
  .btn{
    margin-left: 25%;
    margin-top: 5vh;
  }
  
  .input{
    width: auto;
    margin-left: 0%;
  }
  
  
  </style>