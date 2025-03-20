Convert collections of image data from various file formats to OME-Zarr.


### How to create an OME-Zarr?


<div id="tree"></div>

<script src="https://d3js.org/d3.v7.min.js"></script>
<script>
document.addEventListener("DOMContentLoaded", function() {
  const data = {
    name: "How to create OME-Zarr?",
    children: [
      {
        name: "Unary",
        children: [
          {
            name: "Single File",
            children: [
              {
                name: "Small File (fits in memory)",
                children: [
                  { name: "GUI", children: [
                    { name: "Fiji" },
                    { name: "Fiji, NGFF-Converter" }
                  ]},
                  { name: "Command line", children: [
                    { name: "bioformats2raw" }
                  ]}
                ]
              },
              {
                name: "Large File",
                children: [
                  { name: "GUI", children: [
                    { name: "NGFF-Converter" }
                  ]},
                  { name: "Command line", children: [
                    { name: "bioformats2raw" }
                  ]}
                ]
              }
            ]
          },
          {
            name: "Batch Conversion",
            children: [
              { name: "GUI", children: [
                { name: "NGFF-Converter" }
              ]},
              { name: "Command line", children: [
                { name: "BatchConvert, EuBI-Bridge" }
              ]}
            ]
          }
        ]
      },
      {
        name: "Aggregative",
        children: [
          {
            name: "HCS Dataset",
            children: [
              {
                name: "Companion-OME file",
                children: [
                  { name: "GUI", children: [
                    { name: "NGFF-Converter" }
                  ]},
                  { name: "Command line", children: [
                    { name: "bioformats2raw" }
                  ]}
                ]
              },
              {
                name: "No Companion-OME file",
                children: [
                  { name: "You need to create one!" }
                ]
              }
            ]
          },
          {
            name: "Multi-file Series",
            children: [
              {
                name: "Companion-OME or pattern file available",
                children: [
                  { name: "GUI", children: [
                    { name: "NGFF-Converter" }
                  ]},
                  { name: "Command line", children: [
                    { name: "bioformats2raw" }
                  ]}
                ]
              },
              {
                name: "No Companion-OME or pattern file",
                children: [
                  { name: "EuBI-Bridge" }
                ]
              }
            ]
          }
        ]
      }
    ]
  };

  const width = 600, height = 1000;

  const svg = d3.select("#tree")
      .append("svg")
      .attr("width", width)
      .attr("height", height)
      .append("g")
      .attr("transform", "translate(50,50)");

  const tree = d3.tree()
      .size([height - 100, width - 300])
      .separation((a, b) => (a.parent === b.parent ? 0.7 : 1));

  const root = d3.hierarchy(data);
  tree(root);

  // Shift all nodes to the right
  const shiftRight = 80; // Adjust this value to control the rightward shift
  root.descendants().forEach(d => {
    d.y += shiftRight;
  });

  // Draw links (lines)
  svg.selectAll(".link")
      .data(root.links())
      .enter().append("line")
      .attr("class", "link")
      .attr("x1", d => d.source.y)
      .attr("y1", d => d.source.x)
      .attr("x2", d => d.target.y)
      .attr("y2", d => d.target.x)
      .style("stroke", "red")
      .style("stroke-width", "2px");

  // Draw nodes (circles)
  const node = svg.selectAll(".node")
      .data(root.descendants())
      .enter().append("g")
      .attr("class", "node")
      .attr("transform", d => `translate(${d.y},${d.x})`);
  
  node.append("circle")
      .attr("r", 1)
      .style("fill", "#4285F4");

  // Function to wrap text into multiple lines
  function wrap(text, width) {
    text.each(function() {
      const textElement = d3.select(this);
      const words = textElement.text().split(/\s+/).reverse();
      let word;
      let line = [];
      let lineNumber = 0;
      const lineHeight = 1.1; // ems
      const y = textElement.attr("y");
      const dy = parseFloat(textElement.attr("dy")) || 0;
      let tspan = textElement.text(null).append("tspan").attr("x", 0).attr("y", y).attr("dy", `${dy}em`);
      
      while ((word = words.pop())) {
        line.push(word);
        tspan.text(line.join(" "));
        if (tspan.node().getComputedTextLength() > width) {
          line.pop();
          tspan.text(line.join(" "));
          line = [word];
          tspan = textElement.append("tspan").attr("x", 0).attr("y", y).attr("dy", `${++lineNumber * lineHeight + dy}em`).text(word);
        }
      }
    });
  }

  // Add labels (text) with wrapping and adjusted positioning
  node.append("text")
      .attr("dy", ".31em")
      .attr("x", d => d.children ? -15 : 15)
      .style("text-anchor", d => d.children ? "end" : "start")
      .style("font-size", "12px")
      .style("fill", "blue")
      .text(d => d.data.name)
      .call(wrap, 110)
      .attr("y", function(d) {
        const lines = this.getElementsByTagName('tspan').length;
        return d.children ? -10 * (lines - 1) : 0;
      });
});
</script>





### Modules

- [bioformats2raw](ome_zarr_creation_bf2raw.md)
- [NGFF Converter](ome_zarr_conversion_ngff-converter.md)
- [BatchConvert](ome_zarr_creation_BatchConvert.md)
- [EuBI-Bridge](ome_zarr_creation_EuBI-Bridge.md)
