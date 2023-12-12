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
    let inputvalue = '';

    // Función para manejar el evento de cambio en el campo de entrada.
    // Función para manejar el evento de cambio en el campo de entrada.
    function handleinputvalue(event){
        // Verifica si el tipo del campo es 'date'
        if (type !== 'date') {
            // Almacena el valor del campo de entrada.
            inputvalue = event.target.value;

            // Realiza la validación para evitar valores no permitidos
            const forbiddenValues = ["select", "from", "where","=","or","and","*","-"];

            // Convierte la cadena a minúsculas antes de la comparación
            const lowercaseInput = inputvalue.toLowerCase();

            // Verifica si alguna de las palabras prohibidas está presente en la cadena
            if (forbiddenValues.some(value => lowercaseInput.includes(value))) {
                // Borra el contenido del campo si se encuentra una palabra no permitida
                inputvalue = '';
                event.target.value = '';
                console.log("Se detectó una palabra no permitida. Contenido borrado.");
            }
        }

        // Muestra en la consola el valor del campo de entrada si no está vacío.
        if (inputvalue !== '' || type === 'date') {
            console.log(inputvalue);
        }
    }


    // Variable para almacenar el mensaje de error para Matricula
    let matriculaError = '';

    // Función para manejar el evento de cambio en el campo de Matricula
    function handleMatricula(event) {
        // Almacena el valor del campo de entrada.
        inputvalue = event.target.value;

        // Verifica si la matrícula sigue el formato correcto (4 dígitos seguidos de 3 caracteres)
        const formatoCorrecto = /^[0-9]{4}[a-zA-Z]{3}$/.test(inputvalue);

        // Muestra un mensaje de error si el formato no es correcto.
        if (!formatoCorrecto) {
            matriculaError = 'La matrícula debe seguir el formato: 1234ABC';
            // Borra el contenido del campo de Matrícula cuando aparece el mensaje de error.
            inputvalue = '';
            // Vaciar visualmente el campo de matrícula al encontrar un error
            document.getElementById('Matricula').value = '';
        } else {
            // Convertir las últimas tres letras a mayúsculas si están en minúsculas
            const ultimasTresLetras = inputvalue.slice(-3);
            const ultimasTresLetrasMayusculas = ultimasTresLetras.toUpperCase();
            inputvalue = inputvalue.slice(0, -3) + ultimasTresLetrasMayusculas;
            document.getElementById('Matricula').value = inputvalue.slice(0, -3) + ultimasTresLetrasMayusculas;

            matriculaError = ''; // Restablece el mensaje de error si el formato es correcto.
            // Muestra en la consola el valor del campo de Matrícula si no está vacío.
            if (inputvalue !== '') {
                console.log(inputvalue);
            }
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
{#if requerido === true}
    {#if type === 'date' && id === 'fecha_Entrada'}
        <input id={id} type={type} on:blur={handleinputvalue} name={name} placeholder={name} required value={getFechaActual()}>
    {:else if (type === 'text' && id === 'DNI')}
        <input id={id} type={type} on:blur={handleinputvalue} name={name} placeholder={name} required maxlength={9} on:input={e => inputvalue = e.target.value}>
    {:else}
        <input id={id} type={type} on:blur={handleinputvalue} name={name} placeholder={name} required maxlength={type === 'text' ? 50 : 10} on:input={e => inputvalue = e.target.value}>
    {/if}
{:else}
    <input id={id} type={type} on:blur={handleinputvalue} name={name} placeholder={name} maxlength={type === 'text' ? 50 : 10} on:input={e => inputvalue = e.target.value}>
{/if}



<style>
    /* Estilos para todos los campos de entrada */
input {
    box-sizing: border-box;
    margin-bottom: 15px;
    margin-left: auto;
    margin-right: auto;
    display: block;
    border: 2px solid #000000;
    border-radius: 8px;
    width: 80%;
    padding: 12px;
    transition: box-shadow 0.3s ease;
    font-family: 'Helvetica', sans-serif;
    background-color: #ffffff; /* Color de fondo blanco */
}

/* Estilos para campos de entrada cuando están enfocados */
input:focus {
    outline: none;
    border-color: #007bff; /* Borde de color azul al enfocar */
    box-shadow: 0 0 10px rgba(0, 123, 255, 0.7);
}

/* Estilos para campos de entrada que no están enfocados */
input:not(:focus) {
    background-color: #f5f5f5; /* Fondo gris claro cuando no está enfocado */
    transition: background-color 0.3s ease, opacity 0.3s ease;
}


    /* Estilos específicos para campos de tipo 'date' */
    input[type='date'] {
        box-sizing: border-box;
        margin-bottom: 15px;
        margin-left: auto;
        margin-right: auto;
        display: block;
        border: 2px solid #000000;
        border-radius: 8px;
        width: 80%;
        padding: 12px;
        transition: box-shadow 0.3s ease;
        font-family: 'Helvetica', sans-serif;
        background-color: #ffffff; /* Color de fondo blanco */
        position: relative;
    }
    /* Estilos para campos de entrada de tipo 'date' cuando están enfocados */
    input[type='date']:focus {
        outline: none;
        border-color: #007bff; /* Borde de color azul al enfocar */
        box-shadow: 0 0 10px rgba(0, 123, 255, 0.7);
    }   

    input[type='submit'] {
        width: fit-content;
        padding: 12px 24px;
        font-size: 16px;
        background-color: #4CAF50; /* Verde */
        color: #ffffff; /* Texto en color blanco para mayor contraste */
        border: 2px solid #2d862d; /* Borde verde oscuro */
        display: block; /* Hace que el botón sea un bloque para poder aplicar márgenes automáticos */
        margin: 10px auto; /* Centra el botón horizontalmente */
        cursor: pointer; /* Cambia el cursor al pasar sobre el botón */
        transition: background-color 0.3s ease, border-color 0.3s ease, color 0.3s ease; /* Agrega transiciones para una experiencia más suave */
    }
</style>
