<!--
    Componente de Acompanante:

    Este componente se encarga de mostrar campos adicionales para acompañantes en el formulario principal.
    Cada instancia de este componente representa un acompañante adicional en el formulario.

    Props:
    - numAcompanantes: Número de acompañantes a mostrar.

    Estructura:
    - Un contenedor principal <div> que contiene los campos de entrada para cada acompañante.
    - Utiliza el componente Inputs.svelte para campos de nombre, apellidos y fecha de nacimiento.
    - Utiliza selectores para el sexo y tipo de documento del acompañante.

    Estilos:
    - Estilos aplicados para organizar y presentar visualmente los campos del acompañante.
-->

<script>
    import Inputs from "./Inputs.svelte";

    // Props: numAcompanantes indica la cantidad de acompañantes a mostrar
    export let numAcompanantes;
</script>

<!-- Contenedor principal del componente -->
<div>
    <!-- Verifica si hay acompañantes para mostrar -->
    {#if numAcompanantes > 0}
        <!-- Itera sobre el número de acompañantes especificado -->
        {#each Array(numAcompanantes) as _, i}
            <div>
                <!-- Encabezado del acompañante -->
                <h3>Acompañante {i + 1}</h3>

                <!-- Campos de entrada para Nombre y Apellidos del acompañante -->
                <Inputs name={`Nombre del acompañante ${i + 1}`} id={`Nombre${i + 1}`} type="text" />
                <Inputs name={`Apellidos del acompañante ${i + 1}`} id={`Apellidos${i + 1}`} type="text" />

                <!-- Selector de Sexo del acompañante -->
                <label for={`sexo${i + 1}`}>Sexo</label>
                <select id={`sexo${i + 1}`}>
                    <option value="Masculino">Masculino</option>
                    <option value="Femenino">Femenino</option>
                </select>

                <!-- Selector de Tipo de Documento del acompañante -->
                <label for={`Documento${i + 1}`}>Documento</label>
                <select id={`Documento${i + 1}`}>
                    <option value="DNI">DNI</option>
                    <option value="Pasaporte">Pasaporte</option>
                </select>

                <!-- Campo de entrada para el Número de Documento del acompañante -->
                <Inputs name={`Número documento del acompañante ${i + 1}`} id={`DNI${i + 1}`} type="text" />

                <!-- Etiqueta y campo de fecha de nacimiento del acompañante -->
                <label for="fecha_Nacimiento">Fecha nacimiento <Inputs name="fecha Nacimiento" id={`fecha_Nacimiento${i + 1}`} type="date" requerido=false /></label>
            </div>
        {/each}
    {/if}
</div>

<style>
    /* Estilo para el encabezado de cada acompañante */
    h3 {
        padding-bottom: 10px;
    }

    /* Estilo para el contenedor del selector de Sexo y Tipo de Documento */
    select {
        align-items: center;
        margin-bottom: 10px;
    }

    /* Estilo para la etiqueta del selector */
    label {
        margin-right: 4px;
        margin-left: 10%;

        font-size: 12px;
        display: inline;
    }

    /* Estilo para el selector de Sexo y Tipo de Documento */
    select {
        padding: 5px;
        border: 1px solid #000000;
        border-radius: 4px;
        cursor: pointer;
    }
</style>
