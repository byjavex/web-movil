<!-- Acompanante.svelte -->

<script>
    import Inputs from "./Inputs.svelte";

    export let numAcompanantes = 0;

    function agregarAcompanante() {
        numAcompanantes += 1;
    }

    function eliminarAcompanante() {
        // Verifica si hay acompañantes antes de mostrar el mensaje de confirmación
        if (numAcompanantes > 0) {
            const confirmacion = window.confirm("¿Estás seguro de eliminar el acompañante?");

            if (confirmacion && numAcompanantes > 0) {
                numAcompanantes -= 1;
            }
        }
    }
</script>

<div>
    {#if numAcompanantes > 0}
        {#each Array(numAcompanantes) as _, i}
            <div>
                <h3>Acompañante {i + 1}</h3>
                <Inputs name={`Nombre del acompañante ${i + 1}`} id={`Nombre${i + 1}`} type="text" />
                <Inputs name={`Apellidos del acompañante ${i + 1}`} id={`Apellidos${i + 1}`} type="text" />
                <Inputs name={`DNI del acompañante ${i + 1}`} id={`DNI${i + 1}`} type="text" />
                <label for={`sexo${i + 1}`}>Sexo</label>
                <select id={`sexo${i + 1}`}>
                    <option value="Masculino">Masculino</option>
                    <option value="Femenino">Femenino</option>
                </select>
            </div>
        {/each}
    {/if}

    <!-- Botón para agregar acompañante -->
    <button id = "agregar" type="button" on:click={agregarAcompanante}>Agregar Acompañante</button>

    <!-- Botón para eliminar acompañante, solo si hay acompañantes -->
    {#if numAcompanantes > 0}
        <button id = "eliminar" type="button" on:click={eliminarAcompanante}>Eliminar Acompañante</button>
    {/if}
</div>

<style>
    h3 {
        padding-bottom: 10px;
    }

    #agregar{

        padding: 10px 10px;
        font-size: 16px;
        background-color: #84de59; /* Color de fondo */
        color: #000000; /* Color de texto */
        border: solid   black; /* Sin borde */
        border-radius: 30px; /* Bordes redondeados */
        display: inline-block;
    }

    #eliminar{

        padding: 10px 10px;
        font-size: 16px;
        background-color: rgb(231, 21, 21); /* Color de fondo */
        color: #000000; /* Color de texto */
        border: solid   black; /* Sin borde */
        border-radius: 30px; /* Bordes redondeados */
        display: inline-block;
    }
</style>
