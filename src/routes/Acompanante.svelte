<script>
    import Inputs from "./Inputs.svelte";
    let listaAcompanantes = [];
    for (let i = 0; i < document.getElementById('acompanante').value; i++) {
        listaAcompanantes.push(i);
    }
</script>

{#each listaAcompanantes as persona (persona)}
    <Inputs name={"Nombre" + persona} id={"Nombre" + persona} type="text" />
    <Inputs name={"Apellidos" + persona} id={"Apellidos" + persona} type="text" />
    <Inputs name={"DNI" + persona} id={"DNI" + persona} type="text" />
    <Inputs name={"Tipo_Documento" + persona} id={"Tipo_Documento" + persona} type="text" />
    <Inputs name={"Sexo" + persona} id={"Sexo" + persona} type="text" />

    <!-- Campos de Fecha -->
    <label for={"fecha_Entrada" + persona}>Fecha entrada <Inputs name={"fecha Entrada" + persona} id={"fecha_Entrada" + persona} type="date" /></label>
    <label for={"fecha_Nacimiento" + persona}>Fecha nacimiento <Inputs name={"fecha Nacimiento" + persona} id={"fecha_Nacimiento" + persona} type="date" requerido={false} /></label>
    <label for={"fecha_Expedicion" + persona}>Fecha expedición <Inputs name={"fecha Expedicion" + persona} id={"fecha_Expedicion" + persona} type="date" /></label>
{/each}
