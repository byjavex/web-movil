

<!-- Acompanante.svelte -->

<script >

    import Inputs from "./Inputs.svelte";
    // Crea un store writable para almacenar el número de acompañantes
    export let numAcompanantes = 0

    // Función para agregar campos de acompañante dinámicamente
    function agregarAcompanante() {
        numAcompanantes+=1;  // Incrementa el valor del store
    }

    function eliminarAcompanante() {
        if (numAcompanantes > 0) {
            numAcompanantes -= 1;  // Decrementa el valor del store
        }
    }
</script>

<div>


    <!-- Campos de acompañante dinámicos -->
    {#if numAcompanantes > 0}
        {#each Array(numAcompanantes) as _, i}
            <div>
                <h3>Acompañante {i + 1}</h3>
                <Inputs name={`Nombre del acompañante ${i + 1}`} id={`Nombre${i + 1}`} type="text" />
                <Inputs name={`Apellidos del acompañante ${i + 1}`} id={`Apellidos${i + 1}`} type="text" />
                <Inputs name={`DNI del acompañante ${i + 1}`} id={`DNI${i + 1}`} type="text" />
                <!-- Agrega más campos según sea necesario -->
                <label for={`sexo${i + 1}`}>Sexo</label>
                <select id={`sexo${i + 1}`}>
                    <option value="Masculino">Masculino</option>
                    <option value="Femenino">Femenino</option>
                    <!-- Agrega más opciones según sea necesario -->
                </select>
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
