<script setup>
import { computed } from 'vue'

// 1. Definimos la propiedad que pasaremos desde
// el componente padre
const props = defineProps({
  dataPayment: {
    required: true,
    type: Object,
    default: {
      default: () => ({
        name: '',
        cardNumber: '',
        expirationDate: '',
        securityCode: '',
      })
    }
  }
})

/**
Definimos los los datos y eventos que vamos a emitir al padre

1. update:dataPayment: Mantendrá actualizada la propiedad dataPayment
con el componente padre

2.processDataPayment: Es el evento que enviaremos el padre para avisar
que se puede procesar el pago
*/
const emit = defineEmits([
  'update:dataPayment',
  'processDataPayment'
])

/**
En Vue 3 no puedes modificar directamente el valor de una propiedad
por lo que una de las formas para resolver este problema es a través
de una computada.
En este caso con la función get() obtenemos el valor de la propiedad
dataPayment y con la función set() emitimos al padre los valores
actualizados a través del formulario.
*/
const inputs = computed({
  get: () => props.dataPayment,
  set: (value) => emit('update:dataPayment', value)
})

/** Definimos las variables que vamos a exponer al template html */
defineExpose({
  inputs,
})
</script>

<template>
  <form @submit.prevent="$emit('processDataPayment')" class="form">
    <div class="row">
      <div class="name">
        <label for="ccnum">Full Name</label>
        <input
          placeholder="Full name"
          type="text"
          size="19"
          v-model="inputs.fullName"
        >
      </div>

      <div class="car-number">
        <label for="ccnum">Card Number</label>
        <input
          placeholder="---- ---- ---- ----"
          type="text"
          size="19"
          v-model="inputs.cardNumber"
        >
      </div>

      <div class="expiration">
        <label for="expiry">Expiration</label>
        <input
          placeholder="-- / --"
          size="7"
          type="text"
          v-model="inputs.expirationDate"
        >
      </div>
      <div class="cvc">
        <label for="cvc">CVC</label>
        <input
          placeholder="---"
          size="4"
          type="text"
          v-model="inputs.cvc"
        >
      </div>
    </div>
    <div class="btn-process">
      <button type="submit">Process</button>
    </div>
  </form>
</template>

<style scoped lang="sass">
.form
  max-width: 500px
.row
  display: flex
  flex-wrap: wrap
.name
  max-width: 100%
.card-number
  max-width: 100%
.expiration
  max-width: 100%
.cvc
  max-width: 100%
.btn-process
  margin-top: 10px
</style>
