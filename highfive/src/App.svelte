<script>
    import { _ } from 'svelte-i18n';
    import Stopwatch from "./lib/stopwatch.svelte";
    import Weather from "./lib/weather.svelte";
    import logo from "./assets/logo.png";
    import qr from "./assets/qr-code.svg";
    import Localizator from "./lib/localizator.svelte";
    import ThemeChanger from "./lib/themeChanger.svelte";
    import TechSlider from './lib/sliders/tech.svelte';

</script>

<main>
  <div class="grid">
    <div class="block-1">
      <div>
        <Stopwatch/>
      </div>
      <div>
        <Weather />
      </div>
    </div>
    <div class="block-2">
      <img src="{logo}" style="width: 10vmax;" alt="highfive logo"/>
    </div>
    <div class="block-3">
      <p>{$_('block-3.text')}</p>
    </div>
    <div class="block-4">
      <div class="locale">
        <Localizator/>
      </div>
      <div class="theme">
        <ThemeChanger />
      </div>
      <div style="display: block;" class="slider">
        <TechSlider />
      </div>
      <div class="qr">
        <img src="{qr}" alt="qr code"/>
      </div>
    </div>
    <div class="block-5"></div>
    <div class="block-6"></div>
    <div class="block-7"></div>
    <div class="block-8"></div>
    <div class="block-9"></div>
    <div class="block-10"></div>
    <div class="block-11"></div>
  </div>
</main>

<style>
  .grid{
    /* height: 100%; */
    display: grid;
    grid-template-areas: "block-1 block-2 block-3 block-4" "block-5 block-6 block-7 block-11" "block-8 block-9 block-10 block-11";
    grid-template-columns: 25vw 25vw 25vw 25vw;
    grid-template-rows: repeat(3, 33.3vh);
    max-width: 100vw;
    overflow-x: hidden;
    /* min-height: 100vh; */
  }
  .grid > div{
    padding: 10px;
    overflow: hidden;
  }

  .block-1{
    display: flex;
    flex-direction: row;
    align-items: center;
    justify-content: space-around;
    grid-area: block-1;
    background-color: antiquewhite;
  }
  .block-2{
    display: flex;
    justify-content: center;
    align-items: center;
    grid-area: block-2;
    background-color: aqua;
  }
  .block-3{
    word-break: break-all;
    display: flex;
    justify-content: center;
    align-items: center;
    grid-area: block-3;
    background-color: aquamarine;
    font-size: calc(0.25em + 7.5vmin);
    /* text-align: right; */
  }
  .block-4{
    grid-area: block-4;
    background-color: bisque;
    display: grid;
    gap: 10px;
    grid-template-columns: 50% 50%;
    grid-template-rows: 50% 50%;
  }
  .block-4 div{
    display: flex;
    justify-content: center;
    align-items: center;
  }

  .block-4 img{
    margin: auto;
    max-height: 70%;
  }
  .block-5{
    grid-area: block-5;
    background-color: burlywood;
  }
  .block-6{
    grid-area: block-6;
    background-color: blueviolet;
  }
  .block-7{
    grid-area: block-7;
    background-color: cadetblue;
  }
  .block-8{
    grid-area: block-8;
    background-color: cornflowerblue;
  }
  .block-9{
    grid-area: block-9;
    background-color: darkcyan;
  }
  .block-10{
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: space-around;
    grid-area: block-10;
    background-color: coral;
  }
  .block-11{
    grid-area: block-11;
    background-color: darkseagreen;
  }

  @media(max-width: 1366px){
    .grid{
        grid-template-areas: "block-1 block-2 block-4" "block-6 block-7 block-11" "block-5 block-10 block-11" "block-3 block-8 block-9";
        grid-template-columns: 33.3vw 33.3vw 33.3vw;
        grid-template-rows: repeat(4, 33.3vh);
    }
  }

  @media(max-width: 950px){
    .grid{
        grid-template-areas: "block-2 block-4" "block-6 block-7" "block-1 block-11" "block-10 block-11" "block-8 block-9" "block-5 block-3";
        grid-template-columns: 50vw 50vw;
        grid-template-rows: repeat(6, 50vw);
    }

    .block-1{
      flex-direction: column;
    }

    .block-4 .slider, .block-4 .qr{
      display: none!important;
    }

    .block-4{
      grid-template-columns: 1fr 1fr;
      grid-template-rows: 1fr;
    }
  }
</style>