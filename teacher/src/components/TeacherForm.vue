<script setup lang="ts">
import { ref, type Ref } from 'vue';

const randomId = () => Math.floor(Date.now() * Math.random());

interface ITeacher {
  id: number;
  teacherName: string;
  surName: string;
  dni: string;
  subJects: Array<string>;
  doc: boolean;
}

let teacher: Ref<ITeacher> = ref({
  id: randomId(),
  teacherName: "",
  surName: "",
  dni: "",
  subJects: [],
  doc: false
})
let teachers: Ref<Array<ITeacher>> = ref([]);

let subject: Ref<string> = ref("");

let editando = ref(false);
let teacherIdEditando = ref<number | null>(null);

const handleSubject = () => {
if (subject.value.trim() === "") {
  alert("Complete este campo")
  return;
}
 
 teacher.value.subJects.push(subject.value);
 subject.value = ""
}


const handleTeacher = () => {
  if (editando.value && teacherIdEditando.value !== null) {
    teachers.value = teachers.value.map(item =>
      item.id === teacherIdEditando.value
        ? { ...teacher.value, id: item.id }
        : item
    );
  } else {
    teachers.value.push({
      ...teacher.value,
      id: randomId(),
      subJects: [...teacher.value.subJects]
    });
  }

  teacher.value = {
    id: randomId(),
    teacherName: "",
    surName: "",
    dni: "",
    subJects: [],
    doc: false
  };

  teacherIdEditando.value = null;
  editando.value = false;
};

const deleteTeacher = (dni: ITeacher["dni"]) => {
 teachers.value= teachers.value.filter(teacher => teacher.dni !== dni);
}

const handleEdit = (item: ITeacher) => {
  teacher.value = {
    ...item,
    subJects: [...item.subJects]
  };

  teacherIdEditando.value = item.id;
  editando.value = true;
};

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
 <button @click="handleTeacher()">
  {{ editando ? 'Guardar cambios' : 'Agregar' }}
</button>

  </section>


  <section>
    <h3>Listado de profesores</h3>
    
<table>
  <thead>
    <tr>
      <th>Nombre</th>
      <th>Apellido</th>
      <th>DNI / NIF</th>
      <th>Materias</th>
      <th>Documentación entregada</th>
      <th>Acciones</th>
    </tr>
  </thead>

  <tbody>
    <tr v-if="teachers.length === 0">
      <td colspan="6">No hay profesores aún</td>
    </tr>

    <tr v-for="ele in teachers" :key="ele.id">
      <td>{{ ele.teacherName }}</td>
      <td>{{ ele.surName }}</td>
      <td>{{ ele.dni }}</td>

      <td>
        <ul>
          <li v-for="item in ele.subJects" :key="item">
            {{ item }}
          </li>
        </ul>
      </td>

      <td>
        {{ ele.doc ? 'Entregado' : 'No entregado' }}
      </td>

      <td>
        <button @click="handleEdit(ele)">Editar</button>
        <button @click="deleteTeacher(ele.dni)">Borrar</button>
      </td>
    </tr>
  </tbody>
</table>

  </section>
</template>

<style scoped lang="sass">

$bg: #c6c6c6
$panel: #d4d0c8
$white: #ffffff
$dark: #404040
$black: #222222
$blue: #000080
$teal: #008080
$green: #006400
$red: #800000

*
  box-sizing: border-box

:global(body)
  margin: 0
  padding: 20px
  background: $bg
  color: $black
  font-family: "DejaVu Sans", Arial, sans-serif
  font-size: 13px

section
  max-width: 1000px
  margin: 0 auto 20px
  padding: 3px
  background: $panel
  border: 2px solid
  border-color: $white $dark $dark $white
  box-shadow: 1px 1px 0 $black

  h3
    margin: 0 0 14px
    padding: 9px 10px
    background: $blue
    color: $white
    font-size: 14px
    font-weight: bold
    letter-spacing: 0.4px

  > div
    margin: 10px
    display: flex
    align-items: center
    flex-wrap: wrap
    gap: 8px

  label
    width: 105px
    font-weight: bold

input[type="text"]
  min-width: 0
  flex: 1
  padding: 6px
  background: $white
  color: $black
  border: 2px solid
  border-color: $dark $white $white $dark
  border-radius: 0
  font: inherit

  &:focus
    outline: 1px dotted $black
    outline-offset: -4px

input[type="checkbox"]
  accent-color: $teal

button
  padding: 6px 12px
  background: $panel
  color: $black
  border: 2px solid
  border-color: $white $dark $dark $white
  border-radius: 0
  font: inherit
  cursor: pointer

  &:active
    border-color: $dark $white $white $dark
    padding: 7px 11px 5px 13px

  &:focus-visible
    outline: 1px dotted $black
    outline-offset: -5px

ul
  margin: 4px 0
  padding-left: 24px

li
  margin: 3px 0

table
  width: 100%
  border-collapse: collapse
  background: $white
  border: 2px solid $dark
  text-align: left

th
  padding: 9px 7px
  background: $panel
  border: 1px solid $dark
  border-bottom: 2px solid $dark
  font-weight: bold

td
  padding: 8px 7px
  border: 1px solid #999
  vertical-align: top

tbody tr:nth-child(even)
  background: #e8e6e0

td button
  margin: 2px

td button:first-child
  color: $blue

td button:last-child
  color: $red

@media (max-width: 650px)
  :global(body)
    padding: 8px

  section
    overflow-x: auto

  table
    min-width: 650px

  section > div
    align-items: stretch

  section label
    width: 100%
</style>
