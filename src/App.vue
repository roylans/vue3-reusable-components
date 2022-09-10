<script setup>
import { ref } from 'vue'   

// 1. Importamos el componente
import PaymentCard from './components/PaymentCard.vue';

// 2. Variable reactiva que guardará los datos de tarjeta de pago
const dataPayment = ref({})

// 3. Función que procesará el pago
const processDataPayment = () =>  {
  console.log('Procesamos el pago')
  // const response = await myapi.post(dataPayment)

}
</script>

<template>
  <h1>Procesar Pago</h1>
  <!--
    4. Componente reutilizable para procesar los pagos

    v-model:dataPayment="dataPayment": Pasamos los datos
    al componente a través de la propiedad v-model:dataPayment.
    v-model nos va a permitir tener sincronizados los cambios
    de la propiedad entre el componente padre (App.vue) y el
    hijo(PaymentCard)

    @processDataPayment="processDataPayment": Disparamos un
    evento en el componente hijo (PaymentCard) @processPayment
    y procesamos el pago en el componente padre (App.vue)
    con la función processPayment
  -->
  <PaymentCard
    v-model:dataPayment="dataPayment"
    @processDataPayment="processDataPayment"
  />
</template>

<style scoped>
</style>
