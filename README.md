# Time-series-plots

## Creating time series plots for the Presidency project

```
getwd()
setwd("directory")

text <- data.frame(read.csv("corpus_0524.csv", header = TRUE, sep = ",", na.strings = c("", "NA")))
#access_df <- data.frame(ID = text[[3]], text = as.character(text[[5]]), date = text[[2]], outlet = text[[4]])
corpus_df <- data.frame(ID = text[[2]], text = as.character(text[[3]]), date = text[[4]], outlet = text[[5]])
corpus_df <- corpus_df %>% na.omit()
corpus_df <- corpus_df[!(corpus_df$text == " "),]

date_count <- data.frame(table(clinton_df$date))
write.csv(date_count, "election_clinton_datecount.csv")

podesta <- c(read.csv("election_podesta_datecount_short.csv", header = TRUE, sep = ","))
podesta$date <- as.Date(podesta$date, '%m/%d/%Y')
podesta_count <- data.frame(podesta)
access <- c(read.csv("election_accesshollywood_datecount.csv", header = TRUE, sep = ","))
access$date <- as.Date(access$date, '%Y-%m-%d')
access_count <- data.frame(access)
clinton <- c(read.csv("election_clinton_datecount_short.csv", header = TRUE, sep = ","))
clinton$date <- as.Date(clinton$date, '%m/%d/%Y')
clinton_count <- data.frame(clinton)

podesta_ts <- ts(podesta_count$count, frequency = 1)
access_ts <- ts(access_count$count, frequency = 1)
clinton_ts <- ts(clinton_count$count, frequency = 1)

plot(ts_date, ylab = "number of articles", xlab = "Time from Oct 7")
ggplot(date_count3, aes(date, count)) + geom_line() +
  xlab("") + ylab("Article Count") + labs(title = "Number of Articles per day about Clinton Foundation",
                                          subtitle = "September 30 to November 8")

ts.plot(podesta_ts, access_ts, clinton_ts, gpars = list(col = c("purple","orange","blue")),
        main = "Coverage of Podesta Email Leak (Purple), Access Hollywood (Orange)
        and blue (Clinton Foundation)",
        xlab = "Days from October 1 (news breaks Oct 7)", ylab = "Number of Articles") +
  abline(v=7, col="grey", lty = 2)

seqplot.ts(access_ts, podesta_ts, colx = "red", coly = "blue",
           main = "Coverage of Podesta Email Leak and Access Hollywood",
           xlab = "Days from October 1 (news breaks Oct 7)", ylab = "Number of Articles")
```
