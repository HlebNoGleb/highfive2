<script>
  // @ts-ignore
  import Switch from './switch.svelte';
  import moon from '../assets/moon.png'
  import sun from '../assets/sun.png'


  let themes = [
    {id: "light-theme", icon: sun},
    {id: "dark-theme", icon: moon}
  ]

  let currentTheme = localStorage.getItem("theme");

  if (!currentTheme){
    currentTheme = themes[0].id
    localStorage.setItem("theme", currentTheme);
  }

  function changeTheme(){
    localStorage.setItem("theme", currentTheme);
    document.body.classList.remove(themes[0].id)
    document.body.classList.remove(themes[1].id)
    document.body.classList.add(currentTheme)
  }

  changeTheme();

  let defaultLocale = currentTheme == themes[0].id;

   // @ts-ignore
     $: {
      if (defaultLocale) {
        currentTheme = themes[0].id;
        changeTheme();
      } else {
        currentTheme = themes[1].id
        changeTheme();
      }
    }
</script>
<!-- <select bind:value={currentTheme} on:change={changeTheme}>
    {#each themes as theme}
      <option value={theme}>{theme}</option>
    {/each}
</select> -->

<div class="row">
  <img src="{themes[0].icon}" alt=""/>
    <Switch bind:checked={defaultLocale}/>
  <img src="{themes[1].icon}" alt=""/>
</div>

<style>
  .row{
    align-items: center;
  }

  .row img:nth-child(1){
    margin-right: 10px;
  }

  .row img:nth-child(3){
    margin-left: 10px;
  }

  @media(max-width: 768px){
    .row{
      flex-direction: column;
    }
    .row img:nth-child(1){
      margin-right: 0px;
      margin-bottom: 10px;
    }

    .row img:nth-child(3){
      margin-left: 0px;
      margin-top: 10px;
    }
  }
</style>