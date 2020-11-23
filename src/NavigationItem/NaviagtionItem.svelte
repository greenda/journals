<script>
    export let label = '';
    export let value = '';
    export let onSelect = () => {};

    const selectItem = () => {
        onSelect(value);
    }
</script>

<style>
    h6 {
        cursor: pointer;
    }
</style>

<h6 on:click={selectItem}>{label}</h6>