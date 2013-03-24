# clickme

**clickme** is an R package that plots your R data as interactive JavaScript visualizations.

If you want to go beyond the static plots generated by R, and harness the interactivity and creativity of JavaScript libraries like [D3.js][], you can install clickme and start using JS visualizations as easily as the base `plot()` function.

The variables used in JS visualizations are statically-defined, which makes them hard to customize. Instead of using static JS files, clickme uses **ractives** (short for *interactives*—a hat tip to [Neal Stephenson](https://en.wikipedia.org/wiki/The_Diamond_Age)), which are simple folder structures that contain a template file and some configuration options. This approach makes it easy to specify what input data will be used by the JS code, it improves reusability, and encourages sharing.

Want to learn more? [See the wiki](https://github.com/nachocab/clickme/wiki).

## Quick Usage

You can install clickme by running this in your R session:

```S
install.packages("devtools")
install.packages("knitr", repos = "http://www.rforge.net/", type = "source")

library(devtools)
install_github("clickme", "nachocab")
```

Now you can try the examples:

```S
library(clickme)

# visualize a zoomable phylogenetic tree (OneZoom)
mammals_path <- system.file(file.path("examples", "one_zoom", "data", "mammals.tree"), package="clickme")
clickme(mammals_path, "one_zoom")

# visualize a force-directed interactive graph
items <- paste0("GENE_", 1:40)
n <- 30
df1 <- data.frame(a = sample(items, n, replace = TRUE), b = sample(items, n, replace = TRUE), type = sample(letters[1:3], n, replace=TRUE))
clickme(df1, "force_directed")

# visualize a line plot that allows zooming along the x-axis
n <- 30
cities <- c("Boston", "NYC", "Philadelphia")
df2 <- data.frame(name = rep(cities, each = n), x = rep(1:n, length(cities)), y = c(sort(rnorm(n)), -sort(rnorm(n)),sort(rnorm(n))))
clickme(df2, "line_with_focus")

# visualize an interactive heatmap next to a parallel coordinates plot
df3 <- matrix(rnorm(200), ncol = 8,nrow = 25)
rownames(df3) <- paste0("GENE_", 1:25)
colnames(df3) <- paste0("sample_", 1:8)
clickme(df3, "longitudinal_heatmap") # you will need to have a local server running for this example to work
```

Your browser will open a new tab for each example. They should look something like [this](http://bl.ocks.org/nachocab/5178583).

## Acknowledgements
Thank you **Mike Bostock** for creating the [D3.js][] library. Being able to use it more effectively is the main reason why I developed clickme.

Thank you **Yihui Xie** for building the [knitr][] R package. Even though clickme only uses knitr as a templating engine, it is the most important part of my daily workflow.

## Contributing
If you can see the potential of clickme as a bridge between the R and JS worlds, please contribute by building a ractive, [reporting an issue](https://github.com/nachocab/clickme/issues), or improving the source code.

[D3.js]: http://d3js.org
[knitr]: https://github.com/yihui/knitr


