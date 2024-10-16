<script>
export default{
    props: ["paciente", "fecha", "hora", "motivo"],
};
</script>

<template>   
   <div class="d-flex flex-column border rounded-3 mx-2 p-3 shadow" id="card"> 
        <h5> Paciente </h5>
        <p> {{ paciente }} </p>
        <h5> Fecha </h5>
        <p> {{ fecha }} </p>
        <h5> Hora </h5>
        <p> {{ hora }} </p>        
        <h5> Motivo </h5>
        <p> {{ motivo }} </p>

        <button @click="$emit('eliminarCita')" class="btn btn-light">Eliminar</button>
   </div>
</template>

<style scoped>

#card{
    width: 20vw;
}
</style>