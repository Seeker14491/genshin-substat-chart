<script>
  import { onMount } from "svelte";
  import Highcharts from "highcharts";
  import highchartsMore from "highcharts/highcharts-more";

  highchartsMore(Highcharts);

  export let substatData;

  let chartDiv;

  const palette = [
    "#FA5252",
    "#FD7E14",
    "#FAB005",
    "#82C91E",
    "#228BE6",
    "#7950F2",
  ];

  const lowRoll = substatData.possibleRolls[0];
  const highRoll = substatData.possibleRolls[3];
  const seriesData = palette.map((color, i) => {
    const numRolls = i + 1;
    return {
      x: numRolls,
      low: lowRoll * numRolls,
      high: highRoll * numRolls,
      color
    };
  });

  onMount(() => {
    Highcharts.chart(chartDiv, {
      chart: {
        type: "columnrange",
        inverted: true,
        height: 200,
        spacingRight: 25
      },

      title: {
        text: substatData.displayName,
      },

      xAxis: {
        title: {
          text: "Rolls",
        },
        tickInterval: 1
      },

      yAxis: {
        title: {
          text: `Substat value${substatData.isPercentage ? " (%)" : ""}`,
        },
      },

      tooltip: {
        enabled: false
      },

      plotOptions: {
        columnrange: {
          animation: false,
          dataLabels: {
            enabled: true,
            format: substatData.isPercentage ? "{y:.1f}%" : "{y}",
            crop: false,
            overflow: "allow"
          },
          pointPadding: 0,
          groupPadding: 0,
        },
      },

      legend: {
        enabled: false,
      },

      series: [
        {
          data: seriesData,
        },
      ],
    });
  });
</script>

<div bind:this={chartDiv} />
