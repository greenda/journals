<script>
    import Image from "svelte-image";
    import Part from '../Part/Part.svelte';
    export let article = {};
    export let onMount = () => {};

    let ref;

    $: {
        onMount(article.day, ref);
    }
</script>

<style>
    .article {
        margin-bottom: 52px;
    }
</style>

<div class="article">
    <h3 bind:this={ref}>День {article.day}</h3>
    <h4>{article.date}</h4>
    {#each article.parts as part}
        <Part {part}/>
    {/each}
</div>

