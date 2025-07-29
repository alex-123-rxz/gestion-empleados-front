<template>
  <div id="app">
    <h1>Gestión de Empleados</h1>
    <EmpleadoForm @empleado-creado="actualizarLista" />
    <EmpleadoList ref="lista" />
  </div>
</template>

<script>
import EmpleadoForm from './components/EmpleadoForm.vue'
import EmpleadoList from './components/EmpleadoList.vue'

export default {
  name: 'App',
  components: {
    EmpleadoForm,
    EmpleadoList
  },
  methods: {
    actualizarLista() {
      this.$refs.lista.cargarEmpleados()
    }
  }
}
</script>
