<!--
    Archivo principal:

    Este archivo principal importa varios componentes para construir un formulario.
    Incluye campos de entrada, selectores, un botón de luz y un componente para el envío del formulario.

    Estructura del formulario:
    - Campos de entrada para Nombre, Apellidos, DNI, Ciudad, Email, Dirección, Teléfono y Matrícula.
    - Etiquetas y campos de entrada con tipo "date" para Fecha de Entrada, Fecha de Nacimiento y Fecha de Expedición.
    - Un selector con el nombre "parcela".
    - Un botón de luz.
    - Un componente para el envío del formulario.

    Estilo:
    - Se aplica un estilo mínimo para el diseño general, con un espacio superior de 20px.
-->

<script>
    import Inputs from "./Inputs.svelte";
    import Selector from "./selector.svelte"
    import Envioformulario from "./Envioformulario.svelte";
    import Boton_luz from "./boton_luz.svelte"
</script>

<body>
<div class="main">
    <!-- Campos de Entrada -->
    <Inputs name="Nombre" id="Nombre" type="text"/>
    <Inputs name="Apellidos" id="Apellidos" type="text"/>
    <Inputs name="DNI" id="DNI" type="text"/>
    <Inputs name="Ciudad" id="Ciudad" type="text"/>
    <Inputs name="Email" id="Email" type="text"/>
    <Inputs name="Dirección" id="Direccion" type="text"/>
    <Inputs name="Telefono" id="Telefono" type="text"/>
    <Inputs name="Matricula" id="Matricula" type="text"/>

    <!-- Campos de Fecha -->
    <label>Fecha entrada     <Inputs name="fecha Entrada" id="fecha_Entrada" type="date"/></label>
    <label>Fecha nacimiento   <Inputs name="fecha Nacimiento" id="fecha_Nacimiento" type="date"/></label>
    <label>Fecha expedición   <Inputs name="fecha Expedicion" id="fecha_Expedicion" type="date"/></label>

    <!-- Selector, Botón de Luz y Componente de Envío -->
    <Selector name="parcela"/>
    <Boton_luz/>
    <Envioformulario/>
</div>
</body>

<style>
    /* Estilos generales para el formulario principal */
    .main {
        padding-top: 20px;
    }
</style>


