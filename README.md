# r_txtfrequency_cmd
R commands for running text analysis

// Text Analysis Cleanup Steps in R
//Requirements

// Load and read the data
setwd(~/Desktop/file_name, stringsAsFactors=FALSE)
textblock <- read.csv("file_name.csv")

// Combine all fields (if necessary)
main_text <- paste(text_block$text, collapse=" ")

// Setting up the sources
source_text<- VectorSource(main_text)
corpus_text <- Corpus(source_text)

// Cleaning with the text tm_map //

//convert to lowercase
corpus_text <- tm_map(corpus_text, content_transformer(tolower))
//take out punctation marks
corpus_text <- tm_map(corpus_text, removePuncuation)
//take out white space
corpus_text <- tm_map(corpus_text, stripWhiteSpace)

//remove filler words - conjunctions, prepositions, declaratives
corpus_text <- tm_map(corpus_text, removeWords, stopwords ("english"))

//Generate a document-term matrix DTM
dtm <- DocumentTermMatrix(corpus_text)
dtm_stage <- as.matrix(dtm)

//Find and sort frequency list of words
num_words <- colSum(dtm_stage)
num_words <- sort(num_words, decreasing=TRUE)

head(num_words)
