<script setup>
import { ref } from "vue";

// state
const tasks = ref([]);
const newTask = ref("");

// fungsi tambah tugas
const addTask = () => {
  if (newTask.value.trim() !== "") {
    tasks.value.push(newTask.value);
    newTask.value = "";
  }
};

// fungsi hapus tugas
const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};
</script>

<template>
  <div class="container">
    <h1>To-Do List Vue.js</h1>

    <!-- Form Input Tugas -->
    <form @submit.prevent="addTask" class="task-form">
      <input
        v-model="newTask"
        type="text"
        placeholder="Masukkan tugas baru..."
      />
      <button type="submit">Tambah</button>
    </form>

    <!-- Jika list kosong -->
    <p v-if="tasks.length === 0" class="empty-text">Tidak ada tugas</p>

    <!-- List Tugas -->
    <ul>
      <li v-for="(task, index) in tasks" :key="index" class="task-item">
        {{ task }}
        <button class="delete-btn" @click="deleteTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<style>
.container {
  max-width: 600px;
  margin-top: 40px; 
  font-family: Arial, sans-serif;
  font-size: 20px;
}

body {
  margin: 0;
  padding: 0;
  display: flex;
  justify-content: center; /* hanya tengah horizontal */
  align-items: flex-start; /* konten mulai dari ATAS */
  min-height: 100vh;
  background: #1e1e1e;
}


/* Judul */
h1 {
  text-align: center;
  font-size: 60px;
  margin-bottom: 30px;
}

/* Form Input */
.task-form {
  display: flex;
  gap: 12px;
}

.task-form input {
  flex: 1;
  padding: 14px;           /* Membesarkan box input */
  font-size: 18px;         /* Membesarkan tulisan */
  border-radius: 6px;
}

.task-form button {
  padding: 14px 22px;
  font-size: 18px;
  cursor: pointer;
  border-radius: 6px;
  background: #007bff;
  color: white;
  border: none;
}


/* Item tugas */
.task-item {
  display: flex;
  justify-content: space-between;
  padding: 14px;      
  font-size: 18px;
  margin-top: 12px;
  background: #f1f1f1;
  border-radius: 6px;
  color: #000;
  font-weight: 500;
}

/* Tombol hapus */
.delete-btn {
  background: #ff4d4d;
  border: none;
  padding: 6px 14px;
  font-size: 16px;
  color: white;
  border-radius: 6px;
  cursor: pointer;
}

/* Jika list kosong */
.empty-text {
  margin-top: 20px;
  font-style: italic;
  color: #777;
  text-align: center;
}
</style>
