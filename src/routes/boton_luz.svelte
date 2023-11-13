<!--
    Componente de Checkbox para Luz:

    Este componente define un checkbox que representa el estado de una luz.
    Al hacer clic en el checkbox, el estado cambia y se muestra en la consola.

    Estructura:
    - Una variable (`isChecked`) para almacenar el estado del checkbox (marcado o desmarcado).
    - Una función (`handleClick`) para manejar el evento de clic en el checkbox y actualizar el estado.
    - Un label que contiene el texto "Luz" y un checkbox vinculado al estado (`isChecked`).
    - Al hacer clic en el checkbox, se llama a la función `handleClick` para cambiar el estado y mostrarlo en la consola.

    Estilo:
    - No se aplica ningún estilo específico en este componente.
-->

<script>
    // Variable para almacenar el estado del checkbox (marcado o desmarcado).
    let isChecked = false;

    // Función para manejar el evento de clic en el checkbox.
    function handleClick() {
        // Cambia el estado del checkbox.
        isChecked = !isChecked;

        // Muestra en la consola el estado actual del checkbox.
        console.log(isChecked);
    }
</script>

<!-- Etiqueta y checkbox -->
<label>
    Luz
    <!-- Checkbox vinculado al estado `isChecked` y con un manejador de clic (`handleClick`). -->
    <input id="Luz" type="checkbox" bind:value={isChecked} on:click={handleClick} />
</label>
