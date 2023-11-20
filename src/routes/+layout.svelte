<!--
    Archivo de Encabezado (header):

    Este archivo define la sección de encabezado para un formulario.
    Incluye una imagen, un título y un contenedor para agregar contenido adicional mediante slots.

    Estructura:
    - Una imagen con el id "profile" que sirve como icono o imagen representativa del formulario.
    - Un título principal con el texto "FORMULARIO".
    - Un contenedor para el contenido adicional utilizando slots.

    Estilo:
    - El encabezado tiene una sombra y un fondo verde (#6bec48).
    - El contenido está centrado y espaciado uniformemente.
    - La imagen tiene un tamaño de 10rem x 10rem.
    - El tamaño de la fuente es de 12px.
-->

<script>
    // Importa el archivo de estilos externo (style.css).
    import "./style.css";
</script>

<header>
    <div>
        <!-- Imagen representativa del formulario -->
        <img id="profile" src="/iconito.svg" alt="imagen_software">

        <!-- Título principal del formulario -->
        <h1>FORMULARIO</h1>
    </div>
</header>

<!-- Slot para agregar contenido adicional -->
<slot/>

<style>
    /* Estilos para el encabezado */
    div {
        border-bottom: 2px solid black;
        background-color: #9BE8D8;
        width: 100%;
        height: 7rem;
        display: flex;
        align-items: center;
        justify-content: space-evenly;
        padding-inline: -1px; /* Ajusta el valor según tus necesidades */
        font-size: 12px;
    }

    /* Estilos para la imagen de perfil */
    #profile {
        padding-bottom: 15px;
        width: 10rem;
        height: 10rem;
    }
    h1{
        font-family: "JetBrains Mono ExtraBold";
    }
    /* Media query para pantallas de hasta 600px (puedes ajustar este valor según tus necesidades) */
    @media only screen and (max-width: 600px) {
        div {
            height: 10%; /* Ajusta la altura automáticamente en dispositivos móviles */
            width: auto;
            font-size: 9px;

        }

        #profile {
            width: 30%; /* Ajusta el tamaño de la imagen según tus necesidades */
            height: auto; /* Ajusta la altura automáticamente en dispositivos móviles */
        }
    }

    @media only screen and (max-width: 200px) {
        div {
            font-size: 6px;
        }

        #profile {
            width: 30%; /* Ajusta el tamaño de la imagen según tus necesidades */
            height: auto; /* Ajusta la altura automáticamente en dispositivos móviles */
        }
    }

</style>
