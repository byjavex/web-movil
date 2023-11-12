<script>
    import Inputs from "./Inputs.svelte";
    import Selector from "./selector.svelte"
    import Envioformulario from "./Envioformulario.svelte";
    import Boton_luz from "./boton_luz.svelte"
</script>

<body>
<div class="main">
    <Inputs name="Nombre" id="Nombre" type="text"/>
    <Inputs name="Apellidos" id="Apellidos" type="text"/>
    <Inputs name="DNI" id="DNI" type="text"/>
    <Inputs name="Ciudad" id="Ciudad" type="text"/>

    <Inputs name="Email" id="Email" type="text"/>

    <Inputs name="Dirección" id="Direccion" type="text"/>

    <Inputs name="Telefono" id="Telefono" type="text"/>

    <Inputs name="Matricula" id="Matricula" type="text"/>



    <label>Fecha entrada     <Inputs name="fecha Entrada" id="fecha_Entrada" type="date"/></label>

    <label>Fecha nacimiento   <Inputs name="fecha Nacimiento" id="fecha_Nacimiento" type="date"/></label>

    <label>Fecha expedición     <Inputs name="fecha Expedicion" id="fecha_Expedicion" type="date"/></label>




    <Selector name="parcela"/>
    <Boton_luz/>
    <Envioformulario/>
</div>
</body>

<style>
    .main {
        padding-top: 20px;
    }
</style>
