<!--
For licensing see accompanying LICENSE file.

Copyright (C) 2022 Apple Inc. All Rights Reserved.
-->

<script>
    import { currentCell, spec } from './stores';
    import { scheme } from 'vega-scale';

    const interpolateColors = scheme('lighttealblue');

    export let x = 0;
    export let y = 0;

    export let actual = null;
    export let predict = null;
    export let value = null;
    export let cellSize = 10;

    function mouseover() {
        $currentCell = [actual, predict];
    }

    function mouseout() {
        // eslint-disable-next-line
        $currentCell = null;
    }

    function handleClick() {
        if ($spec.events?.click) {
            $spec.events.click($currentCell);
        }
    }
</script>

<style>
    .outline {
        stroke: #eeeeee;
        pointer-events: all;
    }
</style>

<rect
    on:mouseout={mouseout}
    on:blur={mouseout}
    on:mouseover={mouseover}
    on:focus={mouseover}
    on:click={handleClick}
    class="outline"
    {x} {y}
    width={cellSize}
    height={cellSize}
    fill={interpolateColors(value)}
/>