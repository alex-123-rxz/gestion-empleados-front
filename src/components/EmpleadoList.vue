<template>
  <div>
    <h2>Lista de Empleados</h2>

    <!-- Filtros -->
    <div style="margin-bottom: 1rem;">
      <input v-model="filtroNombre" placeholder="Filtrar por nombre" />
      <input v-model="filtroArea" placeholder="Filtrar por área" />
    </div>

    <!-- Tabla -->
    <table border="1" cellpadding="5">
      <thead>
        <tr>
          <th>Nombre</th>
          <th>Email</th>
          <th>Área</th>
          <th>Fecha de Ingreso</th>
          <th>Estado</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="empleado in empleadosFiltrados" :key="empleado.id">
          <td>{{ empleado.nombre }}</td>
          <td>{{ empleado.email }}</td>
          <td>{{ empleado.area }}</td>
          <td>{{ empleado.fecha_ingreso }}</td>
          <td>{{ empleado.estado }}</td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import api from '../services/api'

export default {
  name: 'EmpleadoList',
  data() {
    return {
      empleados: [],
      filtroNombre: '',
      filtroArea: ''
    }
  },
  computed: {
    empleadosFiltrados() {
      return this.empleados.filter(e => {
        return (
          e.nombre.toLowerCase().includes(this.filtroNombre.toLowerCase()) &&
          e.area.toLowerCase().includes(this.filtroArea.toLowerCase())
        )
      })
    }
  },
  mounted() {
    this.cargarEmpleados()
  },
  methods: {
    async cargarEmpleados() {
      try {
        const response = await api.get('/empleados')
        this.empleados = response.data
      } catch (error) {
        console.error('Error al cargar empleados:', error)
      }
    }
  }
}
</script>
