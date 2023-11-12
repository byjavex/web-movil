<script>
    let isChecked = false;

    //function handleCheckboxChange()
    //Cambia el estado de la flag de la check box que por defecto está en false
    function handleCheckboxChange() {
        isChecked = !isChecked;
    }
</script>

<label> Luz
    <input id="Luz" type="checkbox" bind:checked={isChecked} on:change={handleCheckboxChange} />

</label>