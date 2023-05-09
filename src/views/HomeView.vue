<script setup>
import { ref, onMounted } from 'vue'
import { obtenerTodos, eliminarAlumno } from '../services/alumno.services'
import { resolverGenero } from '../services/Utils'
import NavBar from '../components/NavBar.vue'

const alumnos = ref([])

const eliminar = async (id) => {
  await eliminarAlumno(id)
    .then(() => {
      alumnos.value = [...alumnos.value].filter((al) => al.id !== id);
    })
    .catch(() => alert('Ha ocurrido un error al eliminar el alumno'))
}

onMounted(async () => {
  const obtenerAlumnos = await obtenerTodos()
  alumnos.value = obtenerAlumnos
})
</script>
<template>
  <NavBar />
  <main>
    <div class="bg-light p-5 rounded">
      <table class="table table-hover">
        <thead>
          <tr>
            <th scope="col">No. Control</th>
            <th scope="col">Nombre</th>
            <th scope="col">Apellido Paterno</th>
            <th scope="col">Apellido Materno</th>
            <th scope="col">Edad</th>
            <th scope="col">Género</th>
            <th scope="col">Opciones</th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="{
              id,
              no_control,
              nombre,
              apellido_paterno,
              apellido_materno,
              edad,
              genero
            } in alumnos"
            :key="id"
          >
            <th scope="row">{{ no_control }}</th>
            <td>{{ nombre }}</td>
            <td>{{ apellido_paterno }}</td>
            <td>{{ apellido_materno }}</td>
            <td>{{ edad }}</td>
            <td>{{ resolverGenero(genero) }}</td>
            <td>
              <div class="d-flex gap-3">
                <router-link :to="'/editar/' + id">
                  <button type="button" class="btn btn-warning" id="btnEditar">
                    <i class="bi bi-pencil-square"></i>
                  </button>
                </router-link>
                <button type="button" class="btn btn-danger" id="btnEliminar" @click="eliminar(id)">
                  <i class="bi bi-trash-fill"></i>
                </button>
              </div>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </main>
</template>
