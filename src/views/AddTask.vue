<template>
    <div class="container my-5 add-task-container">
        <h1 class="text-center mb-4">Añadir Tarea</h1>

        <!-- Formulario de entrada -->
        <div class="input-group mb-3">
            <input 
                v-model="newTask" 
                @keyup.enter="addTask" 
                placeholder="Añadir nueva tarea" 
                class="form-control task-input"
            />
            <button @click="addTask" class="btn btn-primary add-button">Añadir</button>
        </div>
        
        <!-- Lista de tareas -->
        <div v-if="tasks.length > 0" class="task-list">
            <div v-for="task in tasks" :key="task.id" class="card task-item mb-2">
                <div class="card-body d-flex justify-content-between align-items-center">
                    <span :class="{ 'text-decoration-line-through text-muted': task.completed }">
                        {{ task.todo }}
                    </span>
                    <div>
                        <button 
                            @click="toggleTaskCompletion(task)" 
                            class="btn btn-sm btn-outline-success me-2"
                        >
                            {{ task.completed ? 'Desmarcar' : 'Completar' }}
                        </button>
                        <button @click="deleteTask(task)" class="btn btn-sm btn-outline-danger">Eliminar</button>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "AddTask",
    data() {
        return {
            newTask: "", // Campo de entrada para la nueva tarea
            tasks: [],   // Lista de tareas locales
        };
    },
    methods: {
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

        // Elimina una tarea específica de la lista
        deleteTask(task) {
            this.tasks = this.tasks.filter((t) => t.id !== task.id);
        },

        // Cambia el estado de la tarea entre completada y no completada
        toggleTaskCompletion(task) {
            task.completed = !task.completed;
        },
    },
};
</script>
<style scoped>
.container {
    max-width: 600px;
}

h1 {
    font-size: 2rem;
    color: #343a40;
}

.task-input {
    font-size: 1rem;
    padding: 0.5rem;
}

.add-button {
    font-size: 1rem;
    font-weight: bold;
}

.task-list {
    margin-top: 20px;
}

.task-item {
    box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
}

.text-decoration-line-through {
    text-decoration: line-through;
}
</style>
