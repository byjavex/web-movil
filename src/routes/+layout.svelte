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
        box-shadow: -1px -1px 10px black;
        background-color: #6bec48;
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
</style>
