<script>

    export let name, id, type


</script>


<input id={id} type={type} name={name} placeholder={name} required>

<style>
    input {
        box-sizing: border-box;
        margin-bottom: 10px;
        border: 2px solid #ccc;
        border-radius: 4px;
        width: 100%; /* Hace que el input ocupe el ancho completo del contenedor */
        padding: 8px;
        transition: box-shadow 0.3s ease; /* Agrega una transición para suavizar la animación */
    }
    input:focus {
        outline: none; /* Elimina el contorno predeterminado al estar enfocado */
        box-shadow: 0 0 10px rgba(0, 123, 255, 0.7); /* Resalta el input cuando está enfocado */
    }
    input:not(:focus) {
        background-color: #e3e3e3; /* Color de fondo apagado para inputs que no están enfocados */
        transition: background-color 0.3s ease, opacity 0.3s ease; /* Agrega transiciones para suavizar los cambios */
    }


</style>

