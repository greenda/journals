<script>
    import NavigationItem from '../NavigationItem/NaviagtionItem.svelte';

    export let articles = {};
    export let onSelect = () => {};

</script>

<style>
    .container {
        text-align: left;
    }

    .container > h4 {
        line-height: 8px;
        margin-top: 0px;
    }
</style>

<div class="container">
    <h4>Содержание</h4>
    {#each articles as article }
        <!-- TODO привязываться не к индексам, а к id -->
        <NavigationItem {onSelect} label={`День ${article.day} - ${article.date}`} value={article.day}/>    
    {/each}
</div>
