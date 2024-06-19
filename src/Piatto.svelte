<script>
    import { objPiatto } from "./store";
    import { idPiatto } from "./store";

    let nome = "";
    let ingredienti = "";

    $: {
        if ($objPiatto) {
            nome = $objPiatto.nome;
            ingredienti = $objPiatto.ingredienti;
        }
    }

    async function updatePiatto(event) {
        event.preventDefault();

        try {
            const res = await fetch(
                `http://localhost:3000/piattiRistorante/${$idPiatto}`,
                {
                    method: "POST",
                    headers: {
                        "Content-Type": "application/json",
                    },
                    body: JSON.stringify({
                        nome: "ciao",
                        ingredienti: "bo",
                        img: "https://www.mcdonalds.it/sites/default/files/styles/product_isolated_preview/public/products/gluten-free-burger_isolated_1%201%20%281%29.png?itok=ygR07HPP",
                    }),
                },
            );
            console.log(res);
            if (res.ok) {
                console.log("Piatto aggiornato con successo");
            } else {
                console.error("Errore nella risposta:", res.statusText);
            }
            console.log(res);
        } catch (error) {
            console.error("Errore nella richiesta:", error);
        }
    }
</script>

<section>
    {#if $objPiatto}
        <form on:submit={updatePiatto}>
            <input type="text" bind:value={nome} />
            <textarea bind:value={ingredienti}></textarea>
            <button type="submit">Modifica Piatto</button>
        </form>
    {:else}
        <p>In attesa..</p>
    {/if}
</section>

<style>
</style>
