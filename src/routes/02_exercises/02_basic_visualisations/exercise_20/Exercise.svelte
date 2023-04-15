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
    import {scaleLinear,scaleOrdinal} from 'd3-scale';
    let xscale = scaleOrdinal()
      .domain(services)
      .range([0,100,200,300,400,500,600]);
    let yscale = scaleLinear()
      .domain([0,3])
      .range([0,innerHeight]);

    import {axisLeft} from 'd3-axis';
    function axisCreator(element){
      const yAxis = axisLeft(yscale);
      yAxis(select(element));
    }
  </script>
  
  <!-- setting a viewBox and max-width allows the SVG to shrink but not grow! -->
  <svg viewbox="0 0 {width} {height}" style="max-width: {width}px">
    <g transform={`translate(${margin.left},${margin.top})`}>
      {#each data as stream}
        <rect x="{xscale(stream.service)}" y="{innerHeight-yscale(stream.viewers)}" width = "50" height = "{yscale(stream.viewers)}"/>
      {/each}
    </g>
    <g transform="translate({0},{margin.top})" use:axisCreator></g>
  </svg>
  