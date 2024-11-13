<!-- src/routes/+layout.svelte -->
<script>
    // Any JavaScript for the layout, if needed
</script>

<style>
    /* Set the background color and text color for the entire site */
    :global(body) {
        background-color: #121212;
        color: #ececf1;
        font-family: Arial, sans-serif;
    }

    nav {
        position: sticky;
        top: 0;
        background-color: #1a1a1a; /* Darker background for the navbar */
        padding: 1rem;
        display: flex;
        justify-content: center;
        gap: 2rem;
        z-index: 1000;
        box-shadow: 0 4px 6px rgba(0, 0, 0, 0.3);
    }
    
    nav a {
        color: #ececf1; /* Light text for contrast */
        text-decoration: none;
        font-size: 1.1rem;
        transition: color 0.3s ease;
    }
    
    nav a:hover {
        color: #a3a3a3; /* Slightly lighter color on hover */
    }
</style>

<nav>
    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/contact">Contact</a>
</nav>

<slot /> <!-- Displays page content for each route -->
