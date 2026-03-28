
# Grad-CAM Attribution Analysis

We analyze node-level attribution using Grad-CAM to understand how different models distribute predictive importance across the graph. Specifically, we measure the cumulative contribution to the prediction as nodes are added in descending order of importance.

A model that concentrates importance on a small fraction of nodes will exhibit a steeper curve (i.e., high cumulative importance achieved with few nodes), indicating stronger locality. In contrast, flatter curves indicate more diffuse, global attribution.

---

## Amazon-Ratings

![Amazon attribution curves](amazon_gradcam_attribution_curves.png)

L2G-Net shows a consistently steeper curve compared to both the Global GFT and Polynormer. This indicates that the model concentrates predictive importance on a smaller subset of nodes. 

The Global GFT exhibits a similar but slightly less localized behavior, while Polynormer distributes importance more uniformly across nodes. This suggests that hierarchical spectral processing encourages selective aggregation, focusing on the most relevant regions of the graph.

---

## Roman-Empire

![Roman attribution curves](roman_gradcam_attribution_curves.png)

The same trend is observed in Roman-Empire. L2G-Net again achieves higher cumulative importance with fewer nodes, indicating stronger locality. 

Compared to Amazon-Ratings, all methods exhibit sharper curves overall, suggesting that the task is more localized in nature. However, L2G-Net still maintains a clear advantage in concentrating predictive signal.

---

## Tolokers

![Tolokers attribution curves](tolokers_gradcam_attribution_curves.png)

Tolokers follows a similar pattern. L2G-Net consistently prioritizes a smaller subset of nodes compared to both the Global GFT and Polynormer. 

Despite the dense and less clearly structured nature of this graph, the hierarchical decomposition still enables selective attribution. This suggests that the locality effect is not tied to a specific graph topology, but rather emerges from the model’s inductive bias.

---

## Discussion

Across all datasets, L2G-Net consistently concentrates predictive importance on fewer nodes than competing methods. This behavior supports the claim that the hierarchical decomposition induces a local-to-global processing scheme:

- **Local spectral filters** extract meaningful structure within subgraphs.
- **Global interactions** are mediated through compact interfaces rather than diffuse propagation.

In contrast:
- **Global GFT** distributes importance more broadly due to its uniform spectral basis.
- **Polynormer** exhibits the most diffuse attribution, consistent with its reliance on attention mechanisms.

These results provide empirical evidence that L2G-Net promotes locality in the decision process, aligning with its design goal of mitigating over-squashing while preserving global reasoning capability.
