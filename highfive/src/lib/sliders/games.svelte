<script>
    import  svelteLogo  from '../../assets/tech/Svelte.svg';
    import  csharp  from '../../assets/tech/csharp.svg';
    import  aspnet  from '../../assets/tech/aspnet.png';
    import Tech from './tech.svelte';
    import Weather from '../weather.svelte';
    import Stopwatch from '../stopwatch.svelte';


    export let callback;
</script>
<!-- svelte-ignore a11y-click-events-have-key-events -->
<swiper-container effect="coverflow" grab-cursor="true" centered-slides="true"
slides-per-view="auto" coverflow-effect-rotate="50" coverflow-effect-stretch="0" coverflow-effect-depth="800"
coverflow-effect-modifier="1" coverflow-effect-slide-shadows="true" observer="true" observeParents="true" autoplay-delay="1000" autoplay-disable-on-interaction="false">
    <swiper-slide on:click={() => {callback(Tech)}}>
      <div style="background-image: url('{svelteLogo}');"></div>
    </swiper-slide>
    <swiper-slide on:click={() => {callback(Stopwatch)}}>
        <div style="background-image: url('{csharp}');"></div>
    </swiper-slide>
    <swiper-slide on:click={() => {callback(Weather)}}>
        <div style="background-image: url('{aspnet}');"></div>
    </swiper-slide>
  </swiper-container>

<style>
    swiper-container{
        height: 100%;
    }
    swiper-slide{
        height: 100%;
        padding: 10px;
    }
    swiper-slide div{
        width: 100%;
        height: 100%;
        background-size: contain;
        background-position: center;
        background-repeat: no-repeat;
    }


</style>
