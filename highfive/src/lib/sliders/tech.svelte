<script>
    import  svelteLogo  from '../../assets/tech/Svelte.svg';
    import  csharp  from '../../assets/tech/csharp.svg';
    import  aspnet  from '../../assets/tech/aspnet.png';
</script>

<swiper-container effect="flip" grab-cursor="true" observer="true" observeParents="true" autoplay-delay="200000" autoplay-disable-on-interaction="false">
    <swiper-slide>
      <div style="background-image: url('{svelteLogo}');"></div>
    </swiper-slide>
    <swiper-slide>
        <div style="background-image: url('{csharp}');"></div>
    </swiper-slide>
    <swiper-slide>
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
