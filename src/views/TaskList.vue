<template>
    <div class="container mt-4">
        <h1 class="text-center">Lista de Tareas</h1>
        <button class="btn btn-primary mb-3" @click="fetchTasks">Cargar Tareas</button>
        
        <div v-if="tasks.length > 0">
            <div v-for="task in tasks" :key="task.id" class="card mb-2">
                <div class="card-body d-flex justify-content-between aling-items-center">
                    <div>
                        <h5 :style="{ textDecoration: task.completed ? 'line-through' : 'none' }" class="mb-1">
                            {{ task.todo }}
                        </h5>
                        <span class="badge" :class="task.completed ? 'bg-success' : 'bg-warning'">
                            {{ task.completed ? 'Completada' : 'Pendiente' }}
                        </span>
                    </div>
                    <div>
                        <button class="btn btn-sm btn-outline-success me-2" @click="toggleTaskCompletion(task)">
                            {{ task.completed ? 'Desmarcar' : 'Completar' }}
                        </button>
                        <button class="btn btn-sm btn-outline-danger" @click="deleteTask(task)">Eliminar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>

export default {
    name: "TaskList",
    data() {
        return {
            tasks: [], // Almacenamiento local de las tareas traídas de la API
        };
    },
    methods: {
        // Llamada para obtener las tareas desde la API externa
        async fetchTasks() {
            // Aquí deberían realizar la solicitud a la API usando axios o fetch.
            // La URL que usaremos es: https://dummyjson.com/todos

            // Sugerencia: Intentar implementarlo con axios o fetch
            try {
                const response = await fetch('https://dummyjson.com/todos');
                const data = await response.json();
                this.tasks = data.todos;
            } catch (error) {
                console.error("Error al obtener las tareas", error);
            }
        },

        // Cambiar el estado de una tarea (completada/no completada)
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },

        // Eliminar la tarea seleccionada
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },
    },
};
</script>

<style scoped>
/* Aquí pueden experimentar con estilos de tu preferencia */
.container {
    max-width: 600px;
}
h1 {
    font-size: 2rem;
    color: #343a40;
}
.card {
    box-shadow: 0px 4px 6px rgba(0, 0, 0, 0.1);
}
</style>