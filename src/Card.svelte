<script>
    import { idPiatto } from "./store";
    import { piattiRistorante } from "./store";
    import { objPiatto } from "./store";

    export let name;
    export let ingredienti;
    export let img;
    export let id;
    let piatto;

    function updatePiatto(id) {
        idPiatto.set(id);
        piatto = $piattiRistorante[$idPiatto];

        objPiatto.set(piatto);

        console.log($objPiatto);
    }
</script>

<div class="card">
    <img src={img} alt={name} />
    <div class="info">
        <h2>{name}</h2>
        <div>
            {ingredienti}
        </div>
    </div>
    <div class="button">
        <button on:click={updatePiatto(id)} type="submit"
            >modifica piatto {id}</button
        >
    </div>
</div>

<style>
    .card {
        width: 20rem;
        border: 1px solid black;
        border-radius: 5px;
    }

    .card img {
        width: 100%;
        border-bottom: 1px solid black;
        background-color: white;
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
    }

    h2 {
        padding-bottom: 1rem;
    }

    .info {
        padding: 1rem;
        word-wrap: break-word;
        overflow-wrap: break-word;
    }

    .button {
        display: flex;
        justify-content: center;
        padding: 1rem 0;
    }
</style>
