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
    - Se aplica un estilo especifico que afecta a la check-box
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
<div class="checkbox-container">
    <label for="Luz" class="checkbox-label">
        <span>Luz</span>
    </label>
    <input id="Luz" type="checkbox" on:click={handleClick} />
</div>

<style>
    /* Contenedor para el checkbox y la etiqueta */
    .checkbox-container {
        display: flex;
        align-items: center;
        margin-bottom: 10px; /* Ajusta según sea necesario */
        margin-top: 10px;
    }

    label {
        margin-right: 10px;
        margin-left: 35px;
    }
    
    span{
        font-family: Helvetica, sans-serif;
        font-weight: bold;
        
    }

    /* Estilo del texto "Luz" */
    .checkbox-container .checkbox-label span {
        margin-right: 10px; /* Espacio entre el texto y el checkbox */
        user-select: none;
    }

    /* Estilo del checkbox */
    .checkbox-container input[type="checkbox"] {
        /* Puedes personalizar estos estilos según tus preferencias */
        appearance: none;
        width: 20px; /* Ancho del checkbox */
        height: 20px; /* Altura del checkbox */
        border: 2px solid #333; /* Borde del checkbox */
        border-radius: 4px; /* Bordes redondeados */
        cursor: pointer;
        pointer-events: auto; /* Habilita la interacción con el checkbox */
    }

    /* Estilo del checkbox cuando está marcado */
    .checkbox-container input[type="checkbox"]:checked {
        background-color: rgb(221, 255, 0); /* Cambia el color de fondo cuando está marcado */
        border-color: #000000; /* Cambia el color del borde cuando está marcado */
    }
</style>
