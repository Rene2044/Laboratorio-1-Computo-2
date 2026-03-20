<script setup>
import { ref, computed } from 'vue';

// --- 5 Variables Reactivas ---
const nombreProducto = ref('');
const precioProducto = ref(0);
const cantidadProducto = ref(1);
const listaCotizacion = ref([]);
const mensajeError = ref('');

// Función para agregar productos con validaciones
const agregarItem = () => {
  // --- Validaciones (Punto 6) ---
  if (nombreProducto.value.trim() === '') {
    mensajeError.value = "El nombre del producto es obligatorio.";
    return;
  }
  if (precioProducto.value <= 0 || cantidadProducto.value <= 0) {
    mensajeError.value = "El precio y la cantidad deben ser mayores a cero.";
    return;
  }

  // Si pasa la validación, agregamos al array
  const nuevoItem = {
    id: Date.now(),
    nombre: nombreProducto.value,
    precio: precioProducto.value,
    cantidad: cantidadProducto.value,
    subtotal: precioProducto.value * cantidadProducto.value
  };

  listaCotizacion.value.push(nuevoItem);
  
  // Limpiar campos y errores
  nombreProducto.value = '';
  precioProducto.value = 0;
  cantidadProducto.value = 1;
  mensajeError.value = '';
};

// Variable computada para el gran total
const totalGeneral = computed(() => {
  return listaCotizacion.value.reduce((acc, item) => acc + item.subtotal, 0);
});
</script>

<template>
  <div class="cotizador">
    <h2>Generador de Cotización Automotriz</h2>

    <form @submit.prevent="agregarItem" class="formulario">
      <div class="campo">
        <label>Producto:</label>
        <input v-model="nombreProducto" type="text" placeholder="Ej. Filtro de aceite">
      </div>

      <div class="campo">
        <label>Precio ($):</label>
        <input v-model.number="precioProducto" type="number" step="0.01">
      </div>

      <div class="campo">
        <label>Cantidad:</label>
        <input v-model.number="cantidadProducto" type="number">
      </div>

      <button type="submit" :disabled="!nombreProducto">Agregar a la Lista</button>
    </form>

    <p v-if="mensajeError" class="error">{{ mensajeError }}</p>

    <hr>

    <table v-if="listaCotizacion.length > 0">
      <thead>
        <tr>
          <th>Producto</th>
          <th>Precio Unit.</th>
          <th>Cant.</th>
          <th>Subtotal</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in listaCotizacion" :key="item.id">
          <td>{{ item.nombre }}</td>
          <td>${{ item.precio.toFixed(2) }}</td>
          <td>{{ item.cantidad }}</td>
          <td>${{ item.subtotal.toFixed(2) }}</td>
        </tr>
      </tbody>
      <tfoot>
        <tr>
          <td colspan="3"><strong>TOTAL COTIZADO:</strong></td>
          <td><strong>${{ totalGeneral.toFixed(2) }}</strong></td>
        </tr>
      </tfoot>
    </table>
    
    <p v-else>No hay productos en la cotización actual.</p>
  </div>
</template>

<style scoped>
.cotizador { max-width: 600px; margin: auto; }
.formulario { display: flex; flex-direction: column; gap: 10px; margin-bottom: 20px; }
.campo { display: flex; justify-content: space-between; }
.error { color: white; background-color: #d9534f; padding: 10px; border-radius: 5px; }
table { width: 100%; border-collapse: collapse; }
th, td { border: 1px solid #ddd; padding: 8px; text-align: left; }
th { background-color: #f2f2f2; }
button { padding: 10px; background-color: #0275d8; color: white; border: none; cursor: pointer; }
button:disabled { background-color: #ccc; }
</style>