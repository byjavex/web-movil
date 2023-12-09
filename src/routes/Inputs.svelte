<!--
    Componente de Entrada (Input):

    Este componente define un campo de entrada de texto o de fecha con estilos y validaciones asociadas.

    Props:
    - name: Nombre del campo de entrada.
    - id: Identificador único del campo de entrada.
    - type: Tipo de campo de entrada (text, date, etc.).

    Estructura:
    - Una variable (`inputvalue`) para almacenar el valor del campo de entrada.
    - Una función (`handleinputvalue`) para manejar el evento de cambio en el campo de entrada y mostrar en la consola el valor cuando se deja de escribir.
    - Un campo de entrada vinculado al valor (`inputvalue`) con un manejador de evento de cambio (`on:blur`) para llamar a la función `handleinputvalue`.
    - Estilos CSS que definen la apariencia del campo de entrada, incluyendo transiciones y efectos visuales.

    Estilos:
    - Se aplica un estilo básico a todos los campos de entrada.
    - Se añaden estilos específicos para campos de tipo `date`.
-->

<script>
    // Importa las props `name`, `id`, y `type` desde el componente padre.
    export let name, id, type, requerido = true;

    // Variable para almacenar el valor del campo de entrada.
    let inputvalue ='';

    // Función para manejar el evento de cambio en el campo de entrada.
    function handleinputvalue(event){
        // Almacena el valor del campo de entrada.
        inputvalue = event.target.value;

        // Muestra en la consola el valor del campo de entrada si no está vacío.
        if (inputvalue !=='') {
            console.log(inputvalue);
        }
    }


    function getFechaActual() {
        const today = new Date();
        const year = today.getFullYear();
        let month = today.getMonth() + 1; // Meses en JavaScript son de 0 a 11
        let day = today.getDate();

        // Agrega un cero delante si el mes o el día es menor que 10
        month = month < 10 ? '0' + month : month;
        day = day < 10 ? '0' + day : day;

        return `${year}-${month}-${day}`;
    }


</script>

<!-- Campo de entrada -->
{#if requerido == true}
    {#if type === 'date' && id === 'fecha_Entrada'}
        <input id={id} type={type} on:blur={handleinputvalue} name={name} placeholder={name} required value={getFechaActual()}>
    {:else }
        <input id={id} type={type} on:blur={handleinputvalue} name={name} placeholder={name} required>
    {/if}
{:else }
    <input id={id} type={type} on:blur={handleinputvalue} name={name} placeholder={name}>
{/if}





<style>
    /* Estilos para todos los campos de entrada */
    input {
        box-sizing: border-box;
        margin-bottom: 10px;
        margin-left: auto;
        margin-right: auto;
        display: block;
        border: 2px solid #000000;
        border-radius: 4px;
        width: 80%;
        padding: 8px;
        transition: box-shadow 0.3s ease;
    }

    /* Estilos para campos de entrada cuando están enfocados */
    input:focus {
        outline: none;
        box-shadow: 0 0 10px rgba(0, 123, 255, 0.7);
    }

    /* Estilos para campos de entrada que no están enfocados */
    input:not(:focus) {
        background-color: #e3e3e3;
        transition: background-color 0.3s ease, opacity 0.3s ease;
    }

    /* Estilos específicos para campos de tipo 'date' */
    input[type='date']{
        box-sizing: border-box;
        margin-bottom: 10px;
        margin-left: auto;
        margin-right: auto;
        display: block;
        border: 2px solid #000000;
        border-radius: 4px;
        width: 80%;
        padding: 8px;
        transition: box-shadow 0.3s ease;
    }


    input[type='submit']{
        width: fit-content;
        padding: 10px 20px;
        font-size: 13px;
        background-color: #5bcc26; /* Color de fondo */
        color: #000000; /* Color de texto */
        border: solid   black; /* Sin borde */
        border-radius: 30px; /* Bordes redondeados */
        display: block; /* Hace que el botón sea un bloque para poder aplicar márgenes automáticos */
        margin: 10px auto; /* Centra el botón horizontalmente */
    }
</style>
