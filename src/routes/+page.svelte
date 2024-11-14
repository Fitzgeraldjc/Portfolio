<script lang="ts">
    let icon: HTMLButtonElement;
    let isGreenTheme = false; // Theme toggle state

    // Toggle the theme and update the styles when clicked
    function toggleTheme() {
        isGreenTheme = !isGreenTheme;
        updateTheme();
    }

    // Function to apply theme-based styles
    function updateTheme() {
        // Set CSS variables based on the theme
        document.documentElement.style.setProperty(
            '--background-color', 
            isGreenTheme ? 'rgba(12, 240, 185, 0.5)' : '#121212'
        );
        document.documentElement.style.setProperty(
            '--text-color', 
            isGreenTheme ? '#004d40' : '#ececf1'
        );

        // Set the glow color to be the opposite of the current theme
        icon.style.boxShadow = isGreenTheme
            ? '0 0 20px rgba(18, 18, 18, 0.8), 0 0 40px rgba(18, 18, 18, 0.6), 0 0 60px rgba(18, 18, 18, 0.4)' // Dark theme glow in green theme
            : '0 0 20px rgba(12, 240, 185, 0.8), 0 0 40px rgba(12, 240, 185, 0.6), 0 0 60px rgba(12, 240, 185, 0.4)'; // Green theme glow in dark theme
    }

    function handleMouseMove(event: MouseEvent) {
        if (!icon) return;

        const rect = icon.getBoundingClientRect();
        const x = event.clientX - (rect.left + rect.width / 2);
        const y = event.clientY - (rect.top + rect.height / 2);

        const rotateX = (y / rect.height) * 45;
        const rotateY = -(x / rect.width) * 45;

        icon.style.transform = `perspective(500px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.2)`;
    }

    function resetIcon() {
        icon.style.transform = 'perspective(500px) rotateX(0deg) rotateY(0deg) scale(1)';
    }

    // Ensure the glow is applied on mount
    import { onMount } from 'svelte';
    onMount(() => {
        updateTheme();
    });
</script>

<style>
    /* Centered container for title and icon */
    .centered-container {
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        height: 100vh;
        text-align: center;
        padding-top: -40vh;
        transition: background-color 0.5s ease, color 0.5s ease;
        background-color: var(--background-color);
        color: var(--text-color);
    }

    /* Title styling */
    .title {
        font-size: 3rem;
        margin-bottom: 1rem;
        position: relative;
        top: -15px;
    }

    /* Button (icon) styling with glow effect */
    .icon {
        width: 150px;
        height: 150px;
        border-radius: 50%;
        overflow: hidden;
        cursor: pointer;
        transition: transform 0.1s ease-out, box-shadow 0.2s ease-out;
        background: none;
        border: none;
        padding: 0;
    }

    .icon img {
        width: 100%;
        height: 100%;
        object-fit: cover;
    }
</style>

<div class="centered-container">
    <!-- Title with your name -->
    <h1 class="title">Jacob Fitzgerald</h1>
    
    <!-- Circular icon with button for accessibility and theme toggle -->
    <button 
        class="icon" 
        bind:this={icon} 
        on:mousemove={handleMouseMove} 
        on:mouseleave={resetIcon} 
        on:click={toggleTheme} 
        aria-label="Toggle theme"
    >
        <img src="/images/Fwoggy.jpg" alt="Jake Fitzgerald" />
    </button>
</div>
