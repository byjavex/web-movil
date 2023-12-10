<!--
<script>
    import Inputs from "./Inputs.svelte";
    let listaAcompanantes = [];
    for (let i = 0; i < document.getElementById('clientes').value; i++) {
        listaAcompanantes.push(i);
    }
</script>

{#each listaAcompanantes as persona (persona)}
    <Inputs name={"Nombre" + persona} id={"Nombre" + persona} type="text" />
    <Inputs name={"Apellidos" + persona} id={"Apellidos" + persona} type="text" />
    <Inputs name={"DNI" + persona} id={"DNI" + persona} type="text" />
    <Inputs name={"Tipo_Documento" + persona} id={"Tipo_Documento" + persona} type="text" />
    <Inputs name={"Sexo" + persona} id={"Sexo" + persona} type="text" />


    <label for={"fecha_Entrada" + persona}>Fecha entrada <Inputs name={"fecha Entrada" + persona} id={"fecha_Entrada" + persona} type="date" /></label>
    <label for={"fecha_Nacimiento" + persona}>Fecha nacimiento <Inputs name={"fecha Nacimiento" + persona} id={"fecha_Nacimiento" + persona} type="date" requerido={false} /></label>
    <label for={"fecha_Expedicion" + persona}>Fecha expedición <Inputs name={"fecha Expedicion" + persona} id={"fecha_Expedicion" + persona} type="date" /></label>
{/each}
-->
<!-- Acompanante.svelte -->

<!-- Acompanante.svelte -->

<script>
    import { writable } from 'svelte/store'
    import Inputs from "./Inputs.svelte";
    // Crea un store writable para almacenar el número de acompañantes
    export const numAcompanantes = writable(0);

    // Función para agregar campos de acompañante dinámicamente
    function agregarAcompanante() {
        $numAcompanantes.update(n => n + 1);  // Incrementa el valor del store
    }

    function eliminarAcompanante() {
        $numAcompanantes.update(n => n - 1);  // Decrementa el valor del store
    }
</script>

<div>


    <!-- Campos de acompañante dinámicos -->
    {#if numAcompanantes > 0}
        {#each Array(numAcompanantes) as _, i}
            <div>
                <h3>Acompañante {i + 1}</h3>
                <Inputs name={`Nombre${i}`} id={`Nombre${i}`} type="text"  />
                <Inputs name={`Apellidos${i}`} id={`Apellidos${i}`} type="text"  />
                <Inputs name={`DNI${i}`} id={`DNI${i}`} type="text"  />
                <!-- Agrega más campos según sea necesario -->

            </div>
        {/each}
    {/if}

    <!-- Botón para agregar acompañante -->
    <button type="button" on:click={agregarAcompanante}>Agregar Acompañante</button>
    <button type="button" on:click={eliminarAcompanante}>Eliminar Acompañante</button>


</div>

<style>
    /* Agrega estilos según sea necesario para el componente Acompanante */
</style>
