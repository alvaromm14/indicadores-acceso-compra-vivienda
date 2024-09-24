<script>
    export let xScale;
    export let margin;
    export let innerWidth;
    export let innerHeight;
    export let hoveredDate;
    export let maxDate;

    const handleMousemove = function (e) {
        hoveredDate = xScale.invert(e.offsetX - margin.left);
    };

    const handleMouseleave = function () {
        hoveredDate = maxDate;
    };
</script>

<rect
    class="hover-listener"
    fill="transparent"
    width={innerWidth}
    height={innerHeight}
    on:mousemove={handleMousemove}
    on:mouseleave={handleMouseleave}
/>

<line
    x1={xScale(hoveredDate)}
    x2={xScale(hoveredDate)}
    y1={0}
    y2={innerHeight}
    stroke="black"
    stroke-width="0.6"
    stroke-dasharray="2, 2"
    pointer-events="none"
/>

<style>
    rect {
        cursor: crosshair;
    }
</style>
