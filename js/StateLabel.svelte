<script>
    export let name = "no name";
    export let valid = false;
</script>

<style>
    .label {
        background-color: lightgray;
        margin: 0.5em;
        padding: 0.5em;
        border: 1px solid #000;
    }

    .label-valid {
        background-color: limegreen;
    }
</style>

<span class="label" class:label-valid={valid}>{name}</span>