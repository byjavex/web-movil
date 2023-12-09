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
    - No se aplica ningún estilo específico en este componente.
-->

<script>
    // Importa la prop `name` desde el componente padre.
    export let name;

    // Arreglo para almacenar opciones numéricas del 1 al 70.
    let opciones = [];

    // Genera las opciones automáticamente.
    if(name==='parcela'){
    for (let i = 0; i <= 70; i++) {
        if(i == 0)opciones.push("-")

        else opciones.push(i);
        }
    }
    else if(name==='Tipo-Documento'){
        opciones = ['DNI', 'Pasaporte', 'Carnet de Extranjería'];
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
        }else alert("No has seleccionado parcela")
    }

</script>

<!-- Etiqueta y selector -->
<label for={name}>Nº {name}:
    {#if name == 'Tipo-Documento'}
        <select id={name} name={name} on:blur={handleSelectValue} on:change={handleSelectValue} >
            <!-- Itera sobre las opciones y genera opciones numeradas en el selector. -->
            {#each opciones as opcion (opcion)}
                <option value={opcion}>{opcion}</option>
            {/each}
        </select>
    {:else}
        <select id={name} name={name} on:blur={handleSelectValue}>

            <!-- Itera sobre las opciones y genera opciones numeradas en el selector. -->
            {#each opciones as opcion (opcion)}
                <option value={opcion}>{opcion}</option>
            {/each}
        </select>
    {/if}
</label>
