<template>
  <div class="container hello my-5 p-4S">
    <h3 class="text-center text-secondary mb-4">
      Esta aplicación te permite gestionar tus tareas de manera eficiente. Puedes añadir 
      nuevas tareas manualmente o extraerlas desde una API.
    </h3>

    <h2>Secciones de la Aplicación</h2>
    <ul class="list-unstyled">
        <li class="mb-2">
            <strong>Añadir Tarea:</strong> Permite ingresar nuevas tareas manualmente.
        </li>
        <li class="mb-2">
            <strong>Lista de Tareas:</strong> Muestra todas las tareas extraídas desde la API, permitiendo marcarlas como completadas o eliminarlas.
        </li>
        <li class="mb-2">
            <strong>Vista Combinada:</strong> Combina las funcionalidades de añadir tareas manualmente y ver las tareas de la API al mismo tiempo.
        </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
    font-size: 1.25rem;
    line-height: 1.5;
}

h2 {
    font-size: 1.75rem;
    color: #2c9ca0; 
    margin-top: 2rem;
    font-weight: bold;
}

ul li {
    font-size: 1rem;
    color: #495057; 
    text-align: center
}
</style>
