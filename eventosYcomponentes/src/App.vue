<script >
import Cita from './components/Cita.vue';

export default{
  name: 'App',

  components: {  
     Cita,
  },

  data(){
    return{
      paciente: '',      
      fecha: '', 
      hora: '', 
      gravedad: '',
      motivo: '', 
      citasMedicas:[],
    };    
  },

  methods: {
    agregarCita() {
      const nuevaCita = {
            paciente: this.paciente, 
            fecha: this.fecha, 
            hora: this.hora, 
            gravedad: this.gravedad,
            motivo: this.motivo,           
          };
        this.citasMedicas.push(nuevaCita);

        // limpia los campos
        this.paciente = "";
        this.fecha = "";
        this.hora = "";
        this.gravedad = "";
        this.motivo = "";
    },   
  },
};
</script>

<template>
  <div> 
     <!-- Formulario -->
      <form class="border border-2  rounded-4 p-3" @submit.prevent="agregarCita">
        <div class="row align-items-start"> 
          <div class="mb-3 col" >
            <!-- Paciente -->
            <label :class="{textoEnRojo:!paciente }" for="FormControlInputPaciente" class="form-label fw-bolder"> Paciente</label>
            <input id="FormControlInputPaciente" class="form-control" type="text" v-model="paciente" required>
          </div>
          <div class="mb-3 col">
            <!-- Fecha -->
            <label :class="{textoEnRojo:!fecha }" for="FormControlInputFecha" class="form-label fw-bolder">Fecha</label>
            <input id="FormControlInputFecha" class="form-control" type="date" v-model="fecha" required>
          </div>
          <div class="mb-3 col">
            <!-- Hora -->
            <label :class="{textoEnRojo:!hora }" for="FormControlInputHora" class="form-label fw-bolder">Hora</label>
            <input id="FormControlInputHora" class="form-control" type="time" v-model="hora" required>
          </div>
          <div class="mb-3 col">
            <!-- Gravedad -->
            <label :class="{textoEnRojo:!gravedad }" for="FormControlInputGravedad" class="form-label fw-bolder">Gravedad</label>
            <select id="FormControlInputGravedad" class="form-select  mb-3" v-model="gravedad" required>          
              <option value="Baja">Baja</option>
              <option value="Media">Media</option>
              <option value="Alta">Alta</option>
            </select>       
          </div>
          <div class="mb-3 col">
            <!-- Motivo -->
            <label :class="{textoEnRojo:!motivo }" for="FormControlInputMotivo" class="form-label fw-bolder">Motivo</label>
            <textarea class="form-control" id="FormControlInputMotivo" rows="1" v-model="motivo" required></textarea>
          </div>
      </div>
      <div class="text-center"> 
        <!-- Botón agregar -->
        <button type="submit" class="btn btn-info text-white col-2"
          :disabled="!paciente || !fecha || !hora || !gravedad || !motivo ">
           Agregar
        </button>
      </div>
    </form>
  </div>
  <!-- Contenedor donde se muestran los resutados -->
  <div class="d-flex mt-5 text-center justify-content-center">
    <!-- Mensaje de aviso de No registros -->
    <span v-if="citasMedicas.length == 0" :style="{color: 'red',}"> Aún no hay consultas registradas </span>
    <!-- Contenedor de las Card de citas registradas -->
    <div v-else-if="citasMedicas.length" class="d-flex " > 
      <Cita v-for="(cita, index) in citasMedicas" :key="index"
      :class="{
        gravedadBaja: cita.gravedad == 'Baja',
        gravedadMedia: cita.gravedad == 'Media',
        gravedadAlta: cita.gravedad == 'Alta',        
      }"

      :paciente= "cita.paciente" 
      :fecha= "cita.fecha" 
      :hora= "cita.hora"      
      :motivo= "cita.motivo"
      @eliminarCita="citasMedicas.splice(index, 1)"
    />      
    </div>
  </div>
 
</template>

<style >

.textoEnRojo{
  color: red;
}

.gravedadBaja{
  background-color: lightgreen; 
}

.gravedadMedia{
  background-color: yellow;
}

.gravedadAlta{
  background-color: red;
  color: white;
}

</style>
