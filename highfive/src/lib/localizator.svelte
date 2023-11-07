<script>
    import {locale, locales} from 'svelte-i18n';
    import Switch from './switch.svelte';
    let currentLocale = $locale;
    function changeLocale(){
      console.log(currentLocale);
      localStorage.setItem("locale", currentLocale);
      $locale = currentLocale;
    }

    let defaultLocale = currentLocale == $locales[0];

    $: {
      if (defaultLocale) {
        currentLocale = $locales[0];
        changeLocale()
      } else {
        currentLocale = $locales[1]
        changeLocale()
      }
    }
</script>
<!-- <select bind:value={currentLocale} on:change={changeLocale}>
    {#each $locales as locale}
      <option value={locale}>{locale}</option>
    {/each}
</select> -->
<div class="row">
  <span>{$locales[0]}</span>
    <Switch bind:checked={defaultLocale}/>
  <span>{$locales[1]}</span>
</div>

<style>
  .row{
    align-items: center;
  }

  .row span:nth-child(1){
    margin-right: 10px;
  }

  .row span:nth-child(3){
    margin-left: 10px;
  }

  @media(max-width: 768px){
    .row{
      flex-direction: column;
    }
    .row span:nth-child(1){
      margin-right: 0px;
      margin-bottom: 10px;
    }

    .row span:nth-child(3){
      margin-left: 0px;
      margin-top: 10px;
    }
  }
</style>