<script>
    import { recensioni } from "./store";
    import Recensioni from "./Recensioni.svelte";
    import { onMount } from "svelte";

    let color = false;

    function changeColor() {
        color = !color;
    }

    let recensione = {
        voto: 1,
        testo: "",
        nome: "",
    };

    function submitRecensione(event) {
        event.preventDefault();

        recensioni.update((value) => [
            {
                testo: recensione.testo,
                voto: recensione.voto,
                nome: recensione.nome,
            },

            ...value,
        ]);

        recensione = {
            voto: 1,
            testo: "",
            nome: "",
        };
    }

    onMount(() => {
        async function importRev() {
            try {
                const res = await fetch("http://localhost:3000/recensioni");
                const data = await res.json();

                recensioni.set(data);
            } catch (error) {
                console.error("Errore durante il fetch dei piatti:", error);
            }
        }

        importRev();
    });
</script>

<section id="contact">
    <h1>Lascia una recensione</h1>
    <div class="container-form">
        <form on:submit|preventDefault={submitRecensione}>
            <label>
                Nome <br />
                <input type="text" bind:value={recensione.nome} />
            </label>
            <label>
                Votazione:
                <select bind:value={recensione.voto}>
                    <option>1</option>
                    <option>2</option>
                    <option>3</option>
                    <option>4</option>
                    <option>5</option>
                </select>
            </label>

            <textarea bind:value={recensione.testo}></textarea>
            <button type="submit">Invio</button>
        </form>
    </div>
    <div class="contenitore-recensioni">
        {#each $recensioni as recensione}
            <div class="recensioni">
                <Recensioni>
                    <h3 slot="nome">
                        <button
                            style:color={color ? "red" : "blue"}
                            on:click={changeColor}>{recensione.nome}</button
                        >
                    </h3>
                    <div>Voto: {recensione.voto}</div>
                    <p slot="testo">{recensione.testo}</p>
                </Recensioni>
            </div>
        {/each}
    </div>
</section>

<style>
    #contact {
        width: 80%;
        margin: 0 auto;
        padding-top: 70px;
    }
    h1 {
        text-align: center;
        font-size: 5rem;
    }

    .container-form {
        display: flex;
        justify-content: center;
    }

    form {
        display: flex;
        flex-direction: column;
        align-items: center;
        margin: 5rem 0;
        border: 2px solid black;
        width: 40rem;
        border-radius: 25px;
    }

    label {
        padding: 1rem 0;
        font-size: 2rem;
        text-align: center;
    }

    input {
        margin-top: 1rem;
        font-size: 2rem;
    }

    select {
        font-size: 1rem;
    }

    textarea {
        width: 25rem;
        height: 20rem;
    }

    button {
        margin: 3rem 0;
        font-size: 2rem;
        padding: 0.5rem;
    }

    .contenitore-recensioni {
        display: flex;
        flex-wrap: wrap;
        justify-content: center;
        gap: 2rem;
        padding: 2rem 0;
    }

    .recensioni {
        width: 20rem;
        border: 2px solid black;
        padding: 2rem;
        border-radius: 25px;
        background-color: white;
    }

    .recensioni h3 {
        color: red;
    }

    .recensioni div {
        padding: 1rem 0;
    }

    .recensioni button {
        border: none;
        background-color: white;
        cursor: pointer;
    }
</style>
