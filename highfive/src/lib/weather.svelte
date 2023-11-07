<script>
    import { onMount } from "svelte";
    import Loader from "./loader.svelte";

    onMount(() => {
        navigator.geolocation.getCurrentPosition(success, error)
    })

    let weather = null

    let key = "64136e923c734b40ae404855230711__1"
    let q = "Minsk";

    function success(params) {
        q = `${params.coords.latitude}, ${params.coords.longitude}`;
        getWeather()
    }
    function error(params) {
        getWeather();
    }

    async function getWeather(){
        await new Promise(t=>setTimeout(t, 200));
        const response = await fetch(`http://api.weatherapi.com/v1/current.json?key=${key}&q=${q}&aqi=no`);
        if (response.ok) {
            const data = await response.json();
            weather = data;
            console.log(weather)
        }

    }
</script>

{#if weather}
    <div class="weather">
        <div class="row">
            <img src="{weather.current.condition.icon}" alt="">
            <p>{parseInt(weather.current.temp_c)} °C</p>
        </div>
        <div class="col">
            <span>Ощащается как: <b>{parseInt(weather.current.feelslike_c)} °C</b></span>
            <span>{weather.location.country}, {weather.location.region}</span>
        </div>
    </div>
{:else}
    <!-- <div class="weather">
        <Loader/>
    </div> -->
    <div class="weather">
        <div class="row">
            <img src="https://cdn.weatherapi.com/weather/64x64/night/119.png" alt="">
            <p>{parseInt("10")} °C</p>
        </div>
        <div class="col">
            <span>Ощащается как: <b>{parseInt("12")} °C</b></span>
            <span>{"Belarus"}, {"Minsk"}</span>
        </div>
    </div>
{/if}

<style>
    .weather{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        text-align: center;
    }

    .weather img{
        width: 5vw;
    }

    .weather p{
        font-size: calc(0.25em + 3vmin);
    }

    .weather span{
        font-size: calc(0.25em + 1vmin);
    }

    .row{
        align-items: center;
    }

    @media(max-width: 950px){
        .weather img{
            width: 10vw;
        }

        .weather p{
            font-size: calc(0.25em + 4vmin);
        }

        .weather span{
            font-size: calc(0.25em + 3vmin);
        }
    }
</style>