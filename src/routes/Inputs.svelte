<script>

    export let name

</script>


<input type="text" name="usuario" placeholder={name} required>


<style>
    input {
        box-sizing: border-box;
        margin-bottom: 10px;
        border: 1px solid #ccc;
        border-radius: 4px;
        width: 100%; /* Hace que el input ocupe el ancho completo del contenedor */
        padding: 8px;
    }
</style>