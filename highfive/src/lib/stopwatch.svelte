<script>
    import { formatTime } from "../assets/utisl";
    import { tweened } from "svelte/motion";
    import { readable } from 'svelte/store';

    // set up a readable store which returns the number of milliseconds between the moment the store is subscribed and following an interval
    export const time = readable(0, function start(set) {
        const beginning = new Date();
        const beginningTime = beginning.getTime();

        const interval = setInterval(() => {
            const current = new Date();
            const currentTime = current.getTime();
            set(currentTime - beginningTime);
        }, 10);

        return function stop() {
            // ! forcedly set the readable value to 0 before clearing the interval
            // it seems the store would otherwise retain the last value and the application would stagger from this value straight to 0
            set(0);
            clearInterval(interval);
        };
    });

    let lapse = 0;
	// previous is set to record the time accumulated before the pause button is pressed
    let previous = 0;

    // unsubscribe is set to refer to the function used to unsubscribe from the store
    let unsubscribe;
    unsubscribe = time.subscribe(value => {
      lapse = value + previous;
    });

    // lapse refers to the number of milliseconds in the stopwatch

    // rotation refers to the degrees applied to the minutes dial to have a full rotation for 60 seconds
    // multiply the value by 60 for the seconds dial to have a full rotation every second
    $: rotation = ((lapse / 1000 / 60) * 360) % 360;

    // this is a very imperfect way to have the dials rotate smoothly back to 0
    // set a transition on the minutes and seconds dial, but only when lapse is set to 0
    // remove it when lapse is then more than 0
    let seconds;
    let minutes;
    // to avoid constantly setting transition to none add a boolean to short-circuit the second conditional
    let transitioned;

    // minutes and seconds are undefined by default
    $: if (!lapse && minutes && seconds) {
        minutes.style.transition = "transform 0.2s ease-in-out";
        seconds.style.transition = "transform 0.2s ease-in-out";
        transitioned = false;
    }
    $: if (lapse && !transitioned) {
        minutes.style.transition = "none";
        seconds.style.transition = "none";
        transitioned = true;
    }
</script>

<svg viewBox="0 0 100 100">
    <g transform="translate(50 50)">
        <circle id="dial" cx="0" cy="0" r="42" fill="none" stroke="currentColor" stroke-width="5" stroke-dasharray="0.3 1.898"></circle>
        <use href="#dial" transform="scale(-1 1)"></use>

        <!-- include the number of milliseconds in the rotation of the minutes dial
        1 full rotation for every 60 seconds
        -->
        <g bind:this="{minutes}" transform="rotate({rotation})">
            <g transform="translate(0 -50)">
                <path d="M -2.25 0 h 4.5 l -2.25 2.5 l -2.25 -2.5" fill="currentColor" stroke="currentColor" stroke-width="1" stroke-linejoin="round" stroke-linecap="round"></path>
            </g>
        </g>

        <g transform="translate(0 20)">
            <!-- include the number of milliseconds in the rotation of the minutes dial
            1 full rotation for every single second
            -->
            <g bind:this="{seconds}" transform="rotate({(rotation * 60) % 360})">
                <path d="M 0 -1 v -4.5" fill="none" stroke="currentColor" stroke-width="0.4" stroke-linejoin="round" stroke-linecap="round"></path>
            </g>
            <circle r="7" fill="none" stroke="currentColor" stroke-width="0.4"></circle>
            <circle r="1" fill="none" stroke="currentColor" stroke-width="0.4"></circle>
        </g>

        <text text-anchor="middle" fill="currentColor" dominant-baseline="middle" font-size="12" style="font-weight: 300; letter-spacing: 1px;">
            {formatTime(lapse)}
        </text>
    </g>
</svg>

<style>
    svg {
        font-family: "Roboto Mono", monospace;
        color: rgb(0, 0, 0);
        width: 12vw;
        height: 12vw;
    }

    @media(max-width: 950px){
        svg {
            font-family: "Roboto Mono", monospace;
            color: rgb(0, 0, 0);
            width: 25vw;
            height: 25vw;
        }
  }
</style>