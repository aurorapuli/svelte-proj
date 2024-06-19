<script>
    const scrollToSection = (id) => {
        document.getElementById(id).scrollIntoView({
            behavior: "smooth",
            block: "start",
        });
    };
</script>

<header>
    <h3 class="logo">Ristorante da Bruno</h3>

    <nav>
        <ul>
            <li on:click={() => scrollToSection("home")}><a>Home</a></li>
            <li on:click={() => scrollToSection("menu")}>Menù</li>
            <li on:click={() => scrollToSection("contact")}>Recensioni</li>
        </ul>
    </nav>
    <div class="social">
        <i class="fa-brands fa-instagram"></i>
        <i class="fa-brands fa-facebook"></i>
        <i class="fa-brands fa-twitter"></i>
    </div>
</header>

<style>
    header {
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 0 10rem;
        height: 4rem;
        border-bottom: 4px solid rgba(206, 190, 14, 0.447);
        position: fixed;
        width: 100%;
        top: 0;
        z-index: 10000;
        background-color: #f7e5d5;
    }

    ul {
        display: flex;
        justify-content: space-between;
    }

    li {
        padding: 0 4rem;
        font-size: 1.2rem;
        cursor: pointer;
    }

    i {
        padding: 0 1rem;
        cursor: pointer;
    }
</style>
