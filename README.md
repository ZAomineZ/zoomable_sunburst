# Zoomable Sunburst with Vue

Zoomable Sunburst with d3.JS and Vue 3, this radial space-filling visualization shows the cumulative values of subtrees

![sunburst.png](public%2Fsunburst.png)

Click a node to zoom in, or the center to zoom out

```
    function clicked(event, p)
{
    parent.datum(p.parent || root);

    root.each(d => d.target = {
        x0: Math.max(0, Math.min(1, (d.x0 - p.x0) / (p.x1 - p.x0))) * 2 * Math.PI,
        x1: Math.max(0, Math.min(1, (d.x1 - p.x0) / (p.x1 - p.x0))) * 2 * Math.PI,
        y0: Math.max(0, d.y0 - p.depth),
        y1: Math.max(0, d.y1 - p.depth)
    });

    const t = svg.transition().duration(750);

    path.transition(t)
        .tween("data", d => {
            const i = d3.interpolate(d.current, d.target);
            return t => d.current = i(t);
        })
        .filter(function(d) {
            return +this.getAttribute("fill-opacity") || arcVisible(d.target);
        })
        .attr("fill-opacity", d => arcVisible(d.target) ? (d.children ? 0.6 : 0.4) : 0)
        .attr("pointer-events", d => arcVisible(d.target) ? "auto" : "none")

        .attrTween("d", d => () => arc(d.current));

    label.filter(function(d) {
        return +this.getAttribute("fill-opacity") || labelVisible(d.target);
    }).transition(t)
        .attr("fill-opacity", d => +labelVisible(d.target))
        .attrTween("transform", d => () => labelTransform(d.current));
}
```

![zoomable_sunburst.png](public%2Fzoomable_sunburst.png)

## Installation

1. Clone repository


```bash
git clone https://github.com/blams/zoomable_sunburst.git
```

2. Navigate to the project directory

```bash
cd zoomable_sunburst
```

3. Install dependencies
```bash
npm i
```

4. Execution

```bash
npm run dev
```
