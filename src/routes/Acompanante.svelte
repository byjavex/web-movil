<!-- Acompanante.svelte -->

<script>
    import Inputs from "./Inputs.svelte";
    import { writable } from "svelte/store";

    // Crear un store para numAcompanantes
    export let numAcompanantes;

</script>


<div>
    {#if numAcompanantes > 0}
        {#each Array(numAcompanantes) as _, i}
            <div>
                <h3>Acompañante {i + 1}</h3>
                <Inputs name={`Nombre del acompañante ${i + 1}`} id={`Nombre${i + 1}`} type="text" />
                <Inputs name={`Apellidos del acompañante ${i + 1}`} id={`Apellidos${i + 1}`} type="text" />
                <Inputs name={`DNI del acompañante ${i + 1}`} id={`DNI${i + 1}`} type="text" />
                <label for={`sexo${i + 1}`}>Sexo</label>
                <select id={`sexo${i + 1}`}>
                    <option value="Masculino">Masculino</option>
                    <option value="Femenino">Femenino</option>
                </select>
            </div>
        {/each}
    {/if}


</div>

<style>
    h3 {
        padding-bottom: 10px;
    }


</style>
