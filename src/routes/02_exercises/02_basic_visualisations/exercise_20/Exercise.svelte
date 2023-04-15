<script>
    // Dimensions
    const width = 600;
    const height = 300;
    const margin = { top: 10, right: 10, bottom: 30, left: 60 };
    const innerWidth = width - margin.left - margin.right;
    const innerHeight = height - margin.top - margin.bottom;
  
    // Array
    const data = [
      { service: "Netflix", viewers: 2.9 },
      { service: "Amazon Prime Video", viewers: 1.3 },
      { service: "Disney+", viewers: 2.1 },
      { service: "Hulu", viewers: 0.9 },
      { service: "Apple TV", viewers: 1.1 },
      { service: "Rakuten", viewers: 0.4 }
    ];
    const services = data.map(obj => obj["service"]);
    import {scaleLinear,scaleBand} from 'd3-scale';
    const xscale = scaleBand()
      .domain(services)
      .range([0,innerWidth]).paddingInner(0.8).paddingOuter(0.475);
    const yscale = scaleLinear()
      .domain([0,3])
      .range([0,innerHeight]);

    import {axisLeft,axisBottom} from 'd3-axis';
    import { select} from 'd3-selection';

    function axisCreator(element){
      const yAxis = axisLeft(yscale);
      yAxis(select(element));
    };
  function axisCreator2(element){
      const xAxis = axisBottom(xscale);
      xAxis(select(element));
    };

  </script>
  
  <!-- setting a viewBox and max-width allows the SVG to shrink but not grow! -->
  <svg viewbox="0 0 {width} {height}" style="max-width: {width}px">
    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each data as stream}
        <rect x="{xscale(stream.service)}" y="{innerHeight-yscale(stream.viewers)}" width = "50" height = "{yscale(stream.viewers)}"/>
      {/each}
    </g>
    <g transform="translate({margin.left},{margin.top})" use:axisCreator>
    </g>
    <g transform="translate({0},{margin.top})">
      <text x=10 y={innerHeight/2} style="writing-mode: tb;"> y-axis</text>
    </g>
    <g transform="translate({margin.left},{margin.top+innerHeight})" use:axisCreator2> 
    </g>
  </svg>
