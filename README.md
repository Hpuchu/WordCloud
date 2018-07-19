# WordCloud
how to create wordcloud of twitter data.




library("twitteR")
library("RCurl")
library("base64enc")
library("httr")
library("tm")
library("wordcloud")
consumer_key<-"M3JbO3RxAE9awlEiZJQ9nD3SP"
consumer_secret<-"ac5jaUGbTpFX69sE8txHNnFrqKxVDcHIXEiTqZVcuoaIGEpuIq"
access_token<-"1012563193816743943-1eLgfmzUoLgUixu8AFJ7ujSZaLhHBm"
access_secret<-"au3DgJUAROI2Tx1fzPjV4W7I8d2FpqZQ2cvGoZCScxN4N"
setup_twitter_oauth(consumer_key,consumer_secret,access_token,access_secret)


searchnew<-searchTwitter("Virat Kohli",n=50,lang="en")
searchnew


search_text_vec<-sapply(searchnew,function(x) x$getText())
search_text_vec

search_tm<-Corpus(VectorSource(search_text_vec))
inspect(search_tm)

search_tm_level1<-tm_map(search_tm,removePunctuation)
inspect(search_tm_level1)

search_tm_clean<-tm_map(search_tm_level1,removeNumbers)
inspect(search_tm_clean)

search_tm_clean<-tm_map(search_tm_clean,stripWhitespace)
inspect(search_tm_clean)

search_tm_clean<-tm_map(search_tm_clean,removeWords,stopwords("english"))
inspect(search_tm_clean)

search_tm_clean<-tm_map(search_tm_clean,stripWhitespace)

search_tm_clean<-tm_map(search_tm_clean,content_transformer(tolower))

wordcloud(search_tm_clean,random.order = TRUE,max.words = 50,scale=c(3,0.5),colors=rainbow(50))
