<script>
    export let part = '';
</script>

<style>
    .annotation {
        line-height: 8px;
        font-size: 0.8em;
        font-style: italic;
        text-align: center;
    }

    .imageContainer {
        padding: 0px 16px;
        text-align: center;
    }
</style>

<h5>{part.time}</h5>
{#each part.paragraphes as paragraph}
    <p>{paragraph}</p>
{/each}
{#if part.image}
    <div class="imageContainer">
        <img src={part.image.src} alt={part.image.annotation}/>
    </div>
    
    <p class="annotation">{part.image.annotation}</p>
{/if}