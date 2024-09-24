<script>
    export let data;
    export let xScale;
    export let yScale;
    export let hoveredDate;
    export let innerHeight;
    export let valor;
    import * as d3 from 'd3';

    $: dataBeforeHover = data.filter((d) => d.Fecha <= hoveredDate);

    import { line } from "d3-shape";

    $: lineGenerator = line()
        .x((d) => xScale(d.Fecha))
        .y((d) => yScale(d[valor]));


    $: areaAsequibilidad = d3.area()
        .curve(d3.curveBasis)
        .x(d => xScale(d.Fecha))
        .y0(innerHeight)
        .y1(d => yScale(d[valor]));

</script>

<path
    d={lineGenerator(dataBeforeHover)}
    stroke="steelblue"
    fill="transparent"
    stroke-width={valor === "Asequibilidad" ? "2" : "0.7"}
/>



<path
    d={lineGenerator(data)}
    stroke="steelblue"
    fill="transparent"
    stroke-width={valor === "Asequibilidad" ? "2" : "0.7"}
    opacity=".35"
/>

<path
    d={areaAsequibilidad(dataBeforeHover)}
    fill="steelblue"
    fill-opacity={valor === "Asequibilidad" ? "0.3" : "0.1"}
/>

<path
    d={areaAsequibilidad(data)}
    fill="steelblue"
    fill-opacity={valor === "Asequibilidad" ? "0.1" : "0.05"}
/>