<script setup>
import { reactive } from 'vue'
import { useRouter } from 'vue-router'
import NavBar from '../components/NavBar.vue'
import { agregarAlumno } from '../services/alumno.services'

const router = useRouter()

const nuevoAlumno = reactive({
  no_control: '',
  nombre: '',
  apellido_paterno: '',
  apellido_materno: '',
  edad: '',
  genero: 'F'
})

const guardar = async () => {
  await agregarAlumno(nuevoAlumno)
    .then(() => {
      router.push('/')
    })
    .catch(() => alert('Ha ocurrido un error'))
}
</script>
<template>
  <NavBar />
  <div class="container">
    <main>
      <div class="py-5 text-center">
        <img
          class="d-block mx-auto mb-4"
          src="https://upload.wikimedia.org/wikipedia/commons/thumb/9/9a/Laravel.svg/1200px-Laravel.svg.png"
          alt=""
          width="72"
          height="57"
        />
        <h1>API REST</h1>
        <p class="lead">
          Una API de REST, es una interfaz de programación de aplicaciones que se ajusta a los
          límites de la arquitectura REST y permite la interacción con los servicios web de RESTful.
          En otras palabras, las API le permiten interactuar con una computadora o un sistema para
          obtener datos o ejecutar una función, de manera que el sistema comprenda la solicitud y la
          cumpla.
        </p>
      </div>

      <hr class="my-4" />

      <div>
        <h2 id="titulo" class="text-center">AGREGAR</h2>
        <br />
      </div>

      <div class="">
        <h4 class="mb-3">Datos</h4>
        <form class="needs-validation" @submit.prevent="guardar($event)">
          <div class="row g-3">
            <div class="col-sm-6">
              <label for="lastName" class="form-label">No. Control</label>
              <input
                v-model="nuevoAlumno.no_control"
                type="text"
                class="form-control"
                placeholder="17520228"
                required
              />
              <div class="invalid-feedback">Valid last name is required.</div>
            </div>

            <div class="col-sm-6">
              <label for="firstName" class="form-label">Nombre</label>
              <input
                v-model="nuevoAlumno.nombre"
                type="text"
                class="form-control"
                placeholder="Yare"
                required
              />
              <div class="invalid-feedback">Valid first name is required.</div>
            </div>

            <div class="col-sm-6">
              <label for="lastName" class="form-label">Apellido Paterno</label>
              <input
                v-model="nuevoAlumno.apellido_paterno"
                type="text"
                class="form-control"
                placeholder="Araujo"
                required
              />
              <div class="invalid-feedback">Valid last name is required.</div>
            </div>
            <div class="col-sm-6">
              <label for="lastName" class="form-label">Apellido Materno</label>
              <input
                v-model="nuevoAlumno.apellido_materno"
                type="text"
                class="form-control"
                placeholder="Delgado"
                required
              />
              <div class="invalid-feedback">Valid last name is required.</div>
            </div>
            <div class="col-sm-6">
              <label for="lastName" class="form-label">Edad</label>
              <input
                v-model="nuevoAlumno.edad"
                type="number"
                class="form-control"
                placeholder="25"
                required
              />
              <div class="invalid-feedback">Valid last name is required.</div>
            </div>
            <div class="col-sm-6">
              <label for="lastName" class="form-label">Género</label>
              <select required class="form-select" v-model="nuevoAlumno.genero">
                <option value="M">Masculino</option>
                <option value="F">Femenino</option>
              </select>
              <div class="invalid-feedback">Valid last name is required.</div>
            </div>

            <hr class="my-4" />
            <button class="w-50 btn btn-primary btn-lg botonAgregar" type="submit">Agregar</button>
          </div>
        </form>
      </div>
    </main>

    <footer class="my-5 pt-5 text-muted text-center text-small">
      <p class="mb-1">&copy; 2023 Instituto Tecnológico Nacional de México - Campus Chilpancingo</p>
    </footer>
  </div>
</template>
