<script>
    import {createEventDispatcher} from "svelte";

    const dispatcher = createEventDispatcher();
    export let name = "no name";

    let down = false;

    function click()  {
        down = !down;
        dispatcher('toggled', down);
    }
</script>

<style>
    .toggle-lever {
        height: 10em;
        width: 10em;
    }

    .toggle-lever-active {
        background-color: green;
    }
</style>

<button
        type="button"
        class="toggle-lever"
        class:toggle-lever-active={down}
        on:click={click}>{name}</button>