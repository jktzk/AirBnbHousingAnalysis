#Setting up initial analysis/Data clean/Data merge
#R code:


install.packages('tidyverse')
library(tidyverse)

amenities<-read.csv("C:\\Users\\joshk\\OneDrive\\Documents\\datasets\\amenities.csv",sep=";")
geolocation<-read.csv("C:\\Users\\joshk\\OneDrive\\Documents\\datasets\\geolocation.csv",sep=";")
marketAnalysis<-read.csv("C:\\Users\\joshk\\OneDrive\\Documents\\datasets\\market_analysis.csv",sep=";")
marketAnalysis2019<-read.csv("C:\\Users\\joshk\\OneDrive\\Documents\\datasets\\market_analysis_2019.csv",sep=";")




marketAnalysis2019<-marketAnalysis2019 %>% 
  mutate(unified_id=as.double(str_remove(unified_id,"AIR")))

geolocation<-geolocation %>% 
  mutate(unified_id=as.double(str_remove(unified_id,"AIR")))

amenities<-amenities %>% 
  mutate(unified_id=as.double(str_remove(unified_id,"AIR")))

marketAnalysisFull<-bind_rows(marketAnalysis,marketAnalysis2019)



marketAnalysisFinal<-merge(marketAnalysisFull,geolocation,by=c("unified_id","month"),all.y=FALSE)
marketAnalysisFinal<-merge(marketAnalysisFinal,amenities,by=c("unified_id","month"),all.y=FALSE)

marketAnalysisFinal<-marketAnalysisFinal[,-c(10,11,13,14)]
marketAnalysisFinal<-marketAnalysisFinal %>% mutate(revenue=as.double(gsub(",",revenue,replacement=".")))%>% 
                                             mutate(nightly.rate=as.double(gsub(",",nightly.rate,replacement=".")))%>%
                                             mutate(latitude=as.double(gsub(",",latitude,replacement=".")))%>%
                                             mutate(longitude=as.double(gsub(",",longitude,replacement=".")))%>%
                                             mutate(guests=as.integer(gsub("\\+",guests,replacement="")))
  
marketAnalysisFinal<-na.omit(marketAnalysisFinal)
