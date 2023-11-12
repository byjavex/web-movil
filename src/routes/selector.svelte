<script>
    export let name
    let opciones = [];

    // Genera las opciones automáticamente
    for (let i = 1; i <= 70; i++) {
        opciones.push(i);

    }
</script>

<label for={name}>Nº {name}:
    <select id={name} name={name}>
        {#each opciones as opcion (opcion)}
            <option value={opcion}>{opcion}</option>
        {/each}
    </select>

</label>
