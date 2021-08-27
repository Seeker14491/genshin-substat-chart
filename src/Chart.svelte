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
    const low = lowRoll * (i + 1);
    const high = highRoll * (i + 1);

    return { low, high, color };
  });

  onMount(() => {
    Highcharts.chart(chartDiv, {
      chart: {
        type: "columnrange",
        inverted: true,
        height: 200,
      },

      title: {
        text: substatData.displayName,
      },

      xAxis: {
        categories: ["1", "2", "3", "4", "5", "6"],
        title: {
          text: "Rolls",
        },
      },

      yAxis: {
        title: {
          text: "Substat value",
        },
        // plotLines: [{value: 1000, width: 6, zIndex: 5, color: "#000000"}]
      },

      tooltip: {},

      plotOptions: {
        columnrange: {
          animation: false,
          dataLabels: {
            enabled: true,
            format: substatData.isPercentage ? "{y:.1f}%" : "{y}",
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
          name: "Roll range",
          data: seriesData,
        },
      ],
    });
  });
</script>

<div bind:this={chartDiv} />
