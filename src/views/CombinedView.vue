<template>
    <div class="container mt-4">
        <h1 class="text-center">Lista de Tareas</h1>

        <!-- Formulario para agregar tareas manualmente -->
        <div class="mb-4">
            <input type="text" v-model="newTask" class="form-control" placeholder="Nueva tarea" />
            <button class="btn btn-primary mt-2" @click="addTask">Agregar Tarea</button>
        </div>

        <!-- Lista de tareas -->
        <div v-if="tasks.length > 0">
            <div v-for="task in tasks" :key="task.id" class="card mb-2">
                <div class="card-body d-flex justify-content-between align-items-center">
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
   // Esta sección debe permitir agregar tareas nuevas a la vez que extraer las tareas anteriores de la API
    import axios from 'axios';  

    export default {
        name: "CombinedView",
        data() {
            return {
                tasks: [], // Almacena todas las tareas, incluidas las de la API y las manuales
                newTask: "", // Almacena el texto de la nueva tarea
            };
        },
        mounted() {
        // Llama a la API al montar el componente para cargar las tareas automáticamente
        this.fetchTasks();
        },
        methods: {
            // Llamada para obtener las tareas desde la API externa
            async fetchTasks() {
                try {
                    const response = await axios.get('https://dummyjson.com/todos');
                    this.tasks = [...this.tasks, ...response.data.todos];
                } catch (error) {
                    console.error("Error al obtener las tareas de la API", error);
                }
            },

            // Agregar una nueva tarea manualmente
            addTask() {
                if (this.newTask.trim() === "") return;

                const newTask = {
                    todo: this.newTask,
                    completed: false,
                    id: Date.now(), 
                };

                // Añadir la nueva tarea al inicio de la lista
                this.tasks.unshift(newTask);
                this.newTask = ""; // Limpiar el campo de entrada después de agregar
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
/* Aquí pueden agregar estilos personalizados para el componente. */
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