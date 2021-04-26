# TCR-Repertoire-
The code, in R, for the project report, which splits the dataset into the MAIT Cell dataset, Sample dataset and Control dataset.
A series of graphs are plotted for each dataset, to show the change in the number of TCR-alpha and those that are condisered as MAIT Cells, the change in the frequencies and proportions of MAIT Cells.
Variances for the frequencies and proportions of MAIT Cells are calculated and statistical tests are performed.

library(tidyverse) 
library(ggplot2)           #install ggplot

data_a <- data_tsv_alpha

#converting timepoints to numeric and adding a column to data
tp_week <- rep(100,dim(data_a)[1])
tp_week[which(data_a$timepoint=="BL")] <- 0
tp_split <- strsplit(data_a$timepoint, "U")
i_spl <- which(sapply(tp_split, length)==2)
week <- as.numeric(sapply(tp_split[i_spl], function(x){x[2]}))
tp_week[i_spl] <- week
data_a$tp_week <- tp_week

ggplot(data = total_TCR_alpha2) +
  geom_point(mapping = aes(x = tp_week, y = junction_aa)) +
  labs(title = "Number of TCRs against time", x = "Timepoint(week)", y = "Number of TCRs")#plotting  total no.TCR against numeric timepoint
