<template>
  <div>
    <h2>Crear Nuevo Empleado</h2>
    <form @submit.prevent="crearEmpleado">
      <div>
        <label>Nombre:</label>
        <input v-model="empleado.nombre" required />
      </div>
      <div>
        <label>Email:</label>
        <input v-model="empleado.email" type="email" required />
      </div>
      <div>
        <label>Área:</label>
        <input v-model="empleado.area" required />
      </div>
      <div>
        <label>Fecha de Ingreso:</label>
        <input v-model="empleado.fecha_ingreso" type="date" required />
      </div>
      <div>
        <label>Estado:</label>
        <select v-model="empleado.estado" required>
          <option value="activo">Activo</option>
          <option value="inactivo">Inactivo</option>
        </select>
      </div>
      <button type="submit">Guardar</button>
    </form>
  </div>
</template>

<script>
import api from '../services/api'

export default {
  name: 'EmpleadoForm',
  data() {
    return {
      empleado: {
        nombre: '',
        email: '',
        area: '',
        fecha_ingreso: '',
        estado: 'activo'
      }
    }
  },
  methods: {
    async crearEmpleado() {
      try {
        await api.post('/empleados', { empleado: this.empleado })
        alert('Empleado creado exitosamente')
        this.$emit('empleado-creado') // Para notificar al componente padre si lo usas con EmpleadoList
        this.resetForm()
      } catch (error) {
        alert('Error al crear el empleado')
        console.error(error)
      }
    },
    resetForm() {
      this.empleado = {
        nombre: '',
        email: '',
        area: '',
        fecha_ingreso: '',
        estado: 'activo'
      }
    }
  }
}
</script>
