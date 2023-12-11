<!--
    Componente Selector:

    Este componente genera un selector (dropdown) con opciones numeradas automáticamente.
    Permite al usuario seleccionar un número del 1 al 70.

    Props:
    - name: Nombre del selector, utilizado para etiquetas y atributos asociados.

    Estructura:
    - Un arreglo de opciones numéricas generadas automáticamente del 1 al 70.
    - Un valor (`option_value`) para almacenar la opción seleccionada.
    - Una función (`handleSelectValue`) para manejar el evento de cambio y mostrar en la consola el valor seleccionado cuando se deja de escribir.

    Estilo:
    - Se añade estilo específico para el tipo select.
-->

<script>
    // Importa la prop `name` desde el componente padre.
    export let name;
    // Variable para almacenar el valor por defecto de clientes.
    let defaultValue = 0;

    // Arreglo para almacenar opciones numéricas del 1 al 70.
    let opciones = [];

    // Genera las opciones automáticamente.
    if (name === 'parcela') {
        for (let i = 0; i <= 70; i++) {
            if (i === 0) opciones.push("-")
            else opciones.push(i);
        }
    }

    if (name === 'clientes') {
        for (let i = 0; i <= 5; i++) {
            opciones.push(i);
        }
    }

    // Variable para almacenar el valor seleccionado.
    let option_value = '-';

    // Función para manejar el cambio en el selector.
    function handleSelectValue(event) {
        let aux = option_value;
        aux = event.target.value;
        // Muestra en la consola el valor seleccionado si no está vacío y lo almacena
        if (aux !== "-") {
            option_value = event.target.value;
            console.log(option_value);
        } else alert("No has seleccionado parcela")
    }

    // Función para manejar el cambio en el selector clientes.
    function handleDefaultValue(event) {
        defaultValue = event.target.value;
        console.log(defaultValue);
    }
</script>

<!-- Etiqueta y selector -->
<label for={name}>Nº {name}:
    {#if name === 'clientes'}
        <select id={name} name={name} on:blur={handleDefaultValue} on:change={handleDefaultValue} bind:value={defaultValue} >
            <!-- Itera sobre las opciones y genera opciones numeradas en el selector. -->
            {#each opciones as opcion (opcion)}
                <option value={opcion}>{opcion}</option>
            {/each}
        </select>
    {:else}
        <select id={name} name={name} on:blur={handleSelectValue} style="{name === 'parcela' ? 'margin-bottom: 10px;' : ''}">

            <!-- Itera sobre las opciones y genera opciones numeradas en el selector. -->
            {#each opciones as opcion (opcion)}
                <option value={opcion}>{opcion}</option>
            {/each}
        </select>
    {/if}
</label>

<style>

    label {
        margin-right: 10px;
        margin-left: 10%;
    }

    /* Estilo para el select */
    select {
        padding: 8px;
        border: 1px solid #ccc;
        border-radius: 4px;
        cursor: pointer;
    }
</style>
