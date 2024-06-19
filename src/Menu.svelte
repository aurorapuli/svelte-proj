<script>
    import Card from "./Card.svelte";
    import Piatto from "./Piatto.svelte";
    import { piattiRistorante } from "./store";
    import { onMount } from "svelte";

    onMount(() => {
        async function importDishes() {
            try {
                const res = await fetch(
                    "http://localhost:3000/piattiRistorante",
                );
                const data = await res.json();

                piattiRistorante.set(data);
            } catch (error) {
                console.error("Errore durante il fetch dei piatti:", error);
            }
        }

        importDishes();
    });
</script>

<section id="menu">
    <h2>Esplora il nostro Menù</h2>
    <div class="container-card">
        {#each $piattiRistorante as piatti, id}
            <Card
                name={piatti.nome}
                ingredienti={piatti.ingredienti}
                img={piatti.img}
                {id}
            />
        {/each}
    </div>
    <Piatto />
</section>

<style>
    #menu {
        width: 80%;
        margin: 0 auto;
        display: flex;
        flex-direction: column;
        align-items: center;
        padding-top: 70px;
    }
    h2 {
        font-size: 4rem;
        text-align: center;
        margin-bottom: 4rem;
    }

    .container-card {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 3rem;
    }
</style>
