## Packages
| Package       | Usage                                                                            |
|---------------|----------------------------------------------------------------------------------|
| algorithm     | Required for pseudocode                                                          |
| algorithmicx  | Provides many option for layout of algorithms                                    |
| algpseudocode | Required for pseudocode                                                          |
| amsmath       | Print out math formulas                                                          |
| amssymb       | Provides entended symbol collection                                              |
| amsthm        | Define theorem-like structures                                                   |
| color         | Set font color, text background                                                  |
| enumitem      | Provides environment of enumerate, itemize, description                          |
| float         | Improves the interface for defining floating objects such as figures and tables. |
| geometry      | Customize page layout                                                            |
| graphicx      | Providing a key-value interface for ```\includegraphics``` command               |
| hyperref      | Handle cross-referencing commands                                                |
| listings      | Typeset programming code within latex                                            |
| todonotes     | Add todo notes                                                                   |
| verbatim      | Provides a comment environment                                                   |

## pgfplots
### Plot functions
```
\begin{tikzpicture}
\begin{axis}[axis lines = left, xlabel = $x$, ylabel = {$f(x)$}]

\addplot [domain=-10:10, samples=100, color=red]{x^2 - 2*x - 1};
\addlegendentry{$x^2 - 2x - 1$}

\addplot [domain=-10:10, samples=100, color=blue]{x^2 + 2*x + 1};
\addlegendentry{$x^2 + 2x + 1$}

\end{axis}
\end{tikzpicture}
```
![func](https://sharelatex-wiki-cdn-671420.c.cdn77.org/learn-scripts/images/4/43/Pgfplots4.png)

### Plot data
```
\begin{tikzpicture}
\begin{axis}[
    title={Temperature dependence of CuSO$_4\cdot$5H$_2$O solubility},
    xlabel={Temperature [\textcelsius]},
    ylabel={Solubility [g per 100 g water]},
    xmin=0, xmax=100,
    ymin=0, ymax=120,
    xtick={0,20,40,60,80,100},
    ytick={0,20,40,60,80,100,120},
    legend pos=north west,
    ymajorgrids=true,
    grid style=dashed,
]

\addplot[color=blue, mark=square]
    coordinates {(0,23.1)(10,27.5)(20,32)(30,37.8)(40,44.6)(60,61.8)(80,83.8)(100,114)};
    \legend{CuSO$_4\cdot$5H$_2$O}
    
\end{axis}
\end{tikzpicture}
```
![data](https://sharelatex-wiki-cdn-671420.c.cdn77.org/learn-scripts/images/5/54/Pgfplots2.png)