<script>
    import ToggleLever from "./ToggleLever.svelte";
    import StateLabel from "./StateLabel.svelte";

    const START_PRESSURE = 5100;
    const PRESSURE_FACTORS = [2, 2, 3, 5, 5, 17];

    let pressure = START_PRESSURE;
    let leverSum = 0;

    let leverDown2 = false;
    let leverDown3 = false;
    let leverDown7 = false;
    let leverDown10 = false;

    let leverSumValidPrime = false;
    let leverSumIsDivisor = false;

    function isPrime(sum) {
        const VALID_NUMBERS = [2, 3, 5, 7, 11, 13, 17, 19, 23, 29];

        return VALID_NUMBERS.includes(sum);
    }

    function isDivisor(sum) {
        return (pressure % sum) === 0;
    }

    function pushState() {
        if (leverSumValidPrime && leverSumIsDivisor) {
            pressure /= leverSum;
        } else {
            pressure = START_PRESSURE;
        }
    }

    $: leverSumValidPrime = isPrime(leverSum, pressure);
    $: leverSumIsDivisor = isDivisor(leverSum, pressure);
    $: {
        let sum = 0;

        if (leverDown2) {
            sum += 2;
        }

        if (leverDown3) {
            sum += 3;
        }

        if (leverDown7) {
            sum += 7;
        }

        if (leverDown10) {
            sum += 10;
        }

        leverSum = sum;
    }
</script>

<style>
    .toggle-lever {

    }

    .lever-container {
        display: flex;
    }
</style>

<p>Pressure: {pressure}
    <StateLabel name="Primzahl" valid={leverSumValidPrime}/>
    <StateLabel name="Divisor" valid={leverSumIsDivisor}/>
</p>

<div class="lever-container">
    <ToggleLever name="2" on:toggled={_ => leverDown2 = _.detail}/>
    <ToggleLever name="3" on:toggled={_ => leverDown3 = _.detail}/>
    <ToggleLever name="7" on:toggled={_ => leverDown7 = _.detail}/>
    <ToggleLever name="10" on:toggled={_ => leverDown10 = _.detail}/>

    <button type="button" on:click={pushState}>Ka-tsching</button>
</div>

