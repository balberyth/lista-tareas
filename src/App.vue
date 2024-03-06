<template>
  <div class="container">
    <section class="input-section">
      <input type="text" v-model="actividad" placeholder="Actividad" />
      <input type="date" v-model="fecha" />
    </section>
    <section class="button-section">
      <button class="btn-agregar" @click="agg">Agregar</button>
      <button class="btn-ordenar" @click="ordenar">Ordenar</button>
    </section>

    <section class="checkbox-section">
      <label class="prioridad-label">Prioridad</label>
      <input type="checkbox" class="mycheck" v-model="check" />
    </section>

    <section class="table-section">
      <table>
        <thead>
          <tr>
            <th>Actividad</th>
            <th>Prioridad</th>
            <th>Fecha</th>
            <th>Opción</th>
          </tr>
        </thead>
        <tbody>
          <tr
  v-for="(e, i) in arr"
  :key="i"
  :class="{
    'row-alta': e.checkk === 'Alta',
    'row-baja': e.checkk === 'Baja',
  }"  >
            <td>{{ e.actividad }}</td>
            <td>{{ e.checkk }}</td>
            <td>{{ e.fecha }}</td>
            <td>
              <button @click="elim(i)">Eliminar</button>
            </td>
          </tr>
        </tbody>
      </table>
    </section>
  </div>
</template>

<script setup>
import { ref } from "vue";
import Swal from 'sweetalert2'

let actividad = ref("");
let fecha = ref("");
let check = ref(false);
let arr = ref([]);

function agg() {
      if (!actividad.value || !fecha.value) {
        Swal.fire({
          icon: 'error',
          title: 'Error',
          text: 'Por favor, complete la actividad y la fecha.',
        });
        return;
      }

      let checkk = check.value ? 'Alta' : 'Baja';

      arr.value.push({
        actividad: actividad.value,
        checkk,
        fecha: fecha.value,
      });

      actividad.value = '';
      fecha.value = '';
      check.value = false;
    }
    function ordenar() {
  arr.value.sort((a, b) => {
    const prioridadA = a.checkk === 'Alta' ? 1 : 0;
    const prioridadB = b.checkk === 'Alta' ? 1 : 0;

    return prioridadB - prioridadA;
  });
}

function elim(i) {
  arr.value.splice(i, 1);
}
</script>

<style>
@media (max-width: 500px) {
  .container {
    max-width: 95%;
  }

  .button-section {
    flex-direction: column;
    align-items: center;
    margin-top: 20px;
  }

  .button-section button {
    margin-bottom: 10px;
  }

  .checkbox-section {
    text-align: center;
    margin-top: 20px;
  }

  .checkbox-section input[type="checkbox"] {
    margin: 0 auto;
    display: block;
  }
}

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

:root {
  --blue1: #06283d;
  --blue2: #1363df;
  --blue3: #47b5ff;
  --blue4: #dff6ff;
  --green: #28a745;
  --red: #dc3545;
  --yellow: #ffc107;
}

body {
  background: linear-gradient(to bottom, var(--blue1), var(--blue2));
  min-height: 100vh;
  font-family: "Roboto", sans-serif;
  display: flex;
  justify-content: center;
  align-items: center;
}

.container {
  max-width: 90%;
  width: 800px;
  height: 90vh;
  background-color: hsla(0, 0%, 100%, 0.357);
  border-radius: 20px;
  box-shadow: 0px 0px 20px rgba(0, 0, 0, 0.2);
  padding: 30px;
  box-sizing: border-box;
  margin: 20px;
}

.input-section input[type="text"],
.input-section input[type="date"] {
  padding: 15px;
  margin-right: 20px;
  border-radius: 8px;
  border: 2px solid var(--blue2);
  width: calc(50% - 25px);
  font-size: 16px;
}

.input-section input[type="text"]:focus,
.input-section input[type="date"]:focus {
  outline: none;
  border-color: var(--blue3);
}

.button-section {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: 30px;
}

.button-section button {
  flex: 1;
  padding: 15px;
  border: none;
  border-radius: 8px;
  background-color: var(--green);
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-size: 16px;
  margin-right: 20px;
}

.checkbox-section {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-top: 20px;
}

.prioridad-label {
  margin-bottom: 5px;
}

.mycheck {
  margin-top: 10px;
  transform: scale(1.5);
}
.table-section button {
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  background-color: var(--red);
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-size: 16px;
}

.button-section button:hover {
  background-color: var(--blue3);
}

.table-section table {
  width: 100%;
  border-collapse: collapse;
  margin-top: 30px;
}

.table-section th,
.table-section td {
  padding: 15px;
  text-align: center;
  border-bottom: 2px solid var(--blue2);
  font-size: 18px;
}

.row-alta {
  background-color: var(--yellow);
}

.row-baja {
  background-color: #f8d7da;
}

.table-section button {
  padding: 10px 20px;
  border: none;
  border-radius: 8px;
  background-color: var(--red);
  color: #fff;
  cursor: pointer;
  transition: background-color 0.3s ease;
  font-size: 16px;
}

.table-section button:hover {
  background-color: #c82333;
}
</style>