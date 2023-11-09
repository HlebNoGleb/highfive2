<script>
    export let active = false;
    export let position = null;
    export let component = null;

    import {get_current_component, onMount} from 'svelte/internal'
    const THISComponent = get_current_component()

    function destroySelf(){
        active = false;
        THISComponent.$destroy();
    }

    onMount(() => {
        if (!position) {
            return;
        }
    })
</script>

{#if active}
    <div class="fullscreen-popup"
        style="--width: {position.width}px; --height: {position.height}px; --top: {position.top}px; --left: {position.left}px">
        <div class="popup-cross">
            <button on:click={destroySelf}>close</button>
        </div>
        <div class="popup-container">
            <svelte:component this={component} />
        </div>
    </div>
{/if}

<style>
    .fullscreen-popup{
        position: fixed;
        background-color: red;
        z-index: 99999;
    }

    @media(min-width:768px){
        .fullscreen-popup{
            animation: initAnimationDesctop .5s linear forwards;
        }
    }

    @media(max-width:767px){
        .fullscreen-popup{
            animation: initAnimationMobile .5s linear forwards;
        }
    }

    .popup-container{
        height: 100%;
        display: block;
        opacity: 0;
        animation: opacity .5s .5s linear forwards;
    }

    @keyframes opacity{
        from{
            opacity: 0;
        }
        to{
            opacity: 1;
        }
    }

    @keyframes initAnimationDesctop{
        0%{
            width: var(--width);
            height: var(--height);
            top: var(--top);
            left: var(--left);
        }
        50%{
            top: 0;
            height: 100vh;
            left: var(--left);
            width: var(--width);
        }
        100%{
            width: 100vw;
            height: 100vh;
            top: 0;
            left: 0;
        }
    }

    @keyframes initAnimationMobile{
        0%{
            width: var(--width);
            height: var(--height);
            top: var(--top);
            left: var(--left);
        }
        50%{
            height: var(--height);
            top: var(--top);
            left: 0;
            width: 100vw;
        }
        100%{
            width: 100vw;
            height: 100vh;
            top: 0;
            left: 0;
        }
    }
</style>