<script>
    import "./style.css"
</script>


<header>
    <div>
        <img id ="profile" src="/iconito.svg" alt="imagen_software">
        <h1>FORMULARIO</h1>
    </div>
</header>
<slot/>


<style>

    div {
        box-shadow: -1px -1px 10px black;
        background-color: #6bec48;
        width: 100%;
        height: 7rem;
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding-inline: -1px; /* Ajusta el valor según tus necesidades */
    }



    #profile{
        padding-bottom: 15px;
        width: 10rem;
        height: 10rem;
    }

</style>