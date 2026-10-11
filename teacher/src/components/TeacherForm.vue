<script setup lang="ts">
import { ref, type Ref } from 'vue';

interface ITeacher{
  teacherName: string,
  surName: string,
  dni: string,
  subJects: Array<string>,
  doc: boolean
}

let teacher: Ref<ITeacher> = ref({
  teacherName: "",
  surName: "",
  dni: "",
  subJects: [],
  doc: false
})
let teachers: Ref<Array<ITeacher>> = ref([]);

let subject: Ref<string> = ref("");

const handleSubject = () => {
if (subject.value.trim() === "") {
  alert("Complete este campo")
  return;
}
 
 teacher.value.subJects.push(subject.value);
 subject.value = ""
}

const handleTeacher  = () => {
 teachers.value.push(
{
  teacherName: teacher.value.teacherName,
  surName: teacher.value.surName,
  dni: teacher.value.dni,
  subJects: teacher.value.subJects,
  doc: teacher.value.doc
}
   )
  teacher.value.teacherName = ""
  teacher.value.surName = ""
  teacher.value.dni = ""
  teacher.value.subJects = []
  teacher.value.doc = false
}
</script>

<template>
  <section>
    <h3>Añadir Profesor</h3>
    <div>
      <label>Nombre:</label> <input type="text" v-model="teacher.teacherName">
    </div>
    <div>
      <label>Apellido:</label> <input type="text" v-model="teacher.surName">
    </div>
    <div>
      <label>DNI / NIF:</label> <input type="text" v-model="teacher.dni">
    </div><div>
      <label>Materias:</label> <input type="text" v-model="subject">
      <button @click="handleSubject()">Agregar</button>
    </div>
    <div>
      <ul>
        <li v-for="(elem, index) in teacher.subJects" v-bind:key="index">
          {{elem}}
          </li>
      </ul>
    </div>
      <input type="checkbox" v-model="teacher.doc"> Documentación entregada
      <button @click="handleTeacher()">Agregar</button>
  </section>


  <section>
    <h3>Listado de profesores</h3>
    <table>
      <tr>
        <th>Nombre</th>
        <th>Apellido</th>
        <th>DNI / NFI</th>
        <th>Materias</th>
        <th>Documetanción Entregada</th>
        <th>Acciones</th>
      </tr>
    <tr v-for="ele in teachers" :key="ele.dni">
  <td>{{ ele.teacherName }}</td>
  <td>{{ ele.surName }}</td>
  <td>{{ ele.dni }}</td>
  <td>
    <ul>
      <li v-for="item in ele.subJects" :key="item">{{ item }}</li>
    </ul>
  </td>
  <td v-if="ele.doc">Entregado</td>
  <td v-else>No entregado</td>
  <td>
    <button>Editar</button>
    <button>Borrar</button>
  </td>
</tr>    </table>
  </section>
</template>

<style scoped lang="css">

</style>
