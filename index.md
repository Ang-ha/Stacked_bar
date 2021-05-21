---
title: "Stacked_bar"
output: html_document
---

```{r install and load packages}
library(ggplot2)
library(reshape2)
library(svglite)
```

```{r set working directory}
setwd("C:/Users/Ang-ha/Google Drive/01.Work_Hohenheim/01.Projects/General aging/New_analysis/Graphs/Stacked_bar")
```

```{r colors}
Genus <- c("Allobaculum" = "darkseagreen",
                                "Cutibacterium" = "darkolivegreen",
                                "Duncaniella" = "darkgoldenrod1", 
           "Helicobacter" = "chocolate3", "Lactobacillus" = "cornflowerblue", "Ligilactobacillus" = "navy", "Limosilactobacillus" = "burlywood", "Streptococcus" = "burlywood4", "f_Lachnospiraceae" = "darkred", "f_Muribaculaceae" = "seashell1", "Others" = "azure4", "Acinetobacter" = "skyblue4", "Corynebacterium" = "lightblue", "Muribacter" = "thistle3", "Pseudomonas" = "mediumpurple4", "f_Ruminococcaceae" = "indianred", "Prevotella" = "aquamarine2", "Alistipes" = "aquamarine4", "Brachyspira" = "darkslategray")
```


```{r load the file }
pc <- read.csv("Duodenum_csv.csv", header = TRUE, check.names = FALSE)
```

```{r convert data frame from long to wide}
pcm <- melt(pc, id = c("Genera"))
```

```{r keep the order of samples}
pcm$Genera <- factor(pcm$Genera,levels=unique(pcm$Genera))
```

```{r make the plot}
duodenum <- ggplot(pcm, aes(x = variable, fill = Genera, y = value)) + 
  geom_bar(stat = "identity", colour = "black") +
  theme(axis.text.x = element_text(size = 18, colour = "black", vjust = 0.5, hjust = 0.5, face= "bold"), 
        axis.title.y = element_text(size = 16, face = "bold"), legend.title = element_text(size = 16, face = "bold"), 
        legend.text = element_text(size = 12, face = "bold.italic", colour = "black"), 
        axis.text.y = element_text(colour = "black", size = 12, face = "bold")) + 
  scale_y_continuous(expand = c(0,0)) + 
  labs(x = "Age (Months)", y = "Average Abundance (%)", fill = "Genus") +
  scale_fill_manual(values = Genus)
```

```{r}
duodenum
```
