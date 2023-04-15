<script>
    // Dimensions
    const width = 800;
    const height = 100;
    const margin = { top: 5, right: 5, bottom: 25, left: 5 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const values = [2, 4, 6, 7, 9];

    import {scaleLog} from 'd3-scale';
    const Log = scaleLog()
      .domain([2,9])
      .range([100,700]);
    import {axisBottom} from 'd3-axis';
    import {select} from 'd3-selection';
    const xAxis = axisBottom(Log)
    function myFunction(handle){
      const xAxis = axisBottom(Log)
    }


  </script>
  
  <svg viewBox="0 0 {width} {height}">
    <g transform="translate({margin.left},{margin.top})" use:myFunction>
      {#each values as value}
        <circle cx="{Log(value)}" cy="50" r = 10/>
      {/each}
    </g>

    select('svg g').call(xAxis)
    <g use:myFunction transform="translate(,{margin.top}+{innerHeight})">
      xAxis(select(g))
    </g>
  </svg>
  