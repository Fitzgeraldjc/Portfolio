<script lang="ts">
    let icon: HTMLDivElement;

    function handleMouseMove(event: MouseEvent) {
        if (!icon) return;

        // Get the bounding box of the icon to find its center
        const rect = icon.getBoundingClientRect();
        const x = event.clientX - (rect.left + rect.width / 2); // Distance from the center horizontally
        const y = event.clientY - (rect.top + rect.height / 2); // Distance from the center vertically

        // Scale these distances to create tilt
        const rotateX = (y / rect.height) * 15; // Adjust tilt intensity
        const rotateY = -(x / rect.width) * 15;

        // Apply the 3D rotation based on cursor position and increase glow
        icon.style.transform = `perspective(500px) rotateX(${rotateX}deg) rotateY(${rotateY}deg) scale(1.2)`;
        icon.style.textShadow = `0 0 20px rgba(255, 255, 255, 0.8), 0 0 40px rgba(255, 255, 255, 0.6), 0 0 60px rgba(255, 255, 255, 0.4)`;
    }

    function resetIcon() {
        // Reset the transform and glow when the mouse leaves
        icon.style.transform = 'perspective(500px) rotateX(0deg) rotateY(0deg) scale(1)';
        icon.style.textShadow = '0 0 15px rgba(255, 255, 255, 0.5), 0 0 30px rgba(255, 255, 255, 0.3)';
    }
</script>

<style>
    .centered-container {
        display: flex;
        justify-content: center;
        align-items: center;
        height: 80vh;
        text-align: center;
    }

    .icon {
        font-size: 6rem;
        color: #ececf1;
        /* Base glow effect */
        text-shadow: 0 0 15px rgba(255, 255, 255, 0.5), 0 0 30px rgba(255, 255, 255, 0.3);
        transition: transform 0.1s ease-out, text-shadow 0.2s ease-out; /* Smooth transition for glow */
        cursor: pointer;
        transform-origin: center center;
    }
</style>

<div class="centered-container">
    <div 
        class="icon" 
        bind:this={icon} 
        on:mousemove={handleMouseMove} 
        on:mouseleave={resetIcon} 
        role="img" 
        aria-label="Tilting glowing star icon"
    >
        ⭐
    </div>
</div>
