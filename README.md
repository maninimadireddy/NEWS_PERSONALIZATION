# News Personalization: Leveraging RAG for Targeted Content Delivery

***What is RAG?***

At its core, RAG utilizes a dual-step process to enhance the quality of generated response text. The first crucial component is the *retriever*, a mechanism responsible for processing vast amounts of external non-parametric data (could be a vector store, csv files or even a SQL database) and retrieving contextually appropriate information from a vast knowledge base using dense vector similarity search or traditional information retrieval methods. The second essential component is the *generator*, which is essentially an LLM responsible for creating coherent and contextually relevant response text. Unlike traditional generative models, the RAG generator is conditioned not only on the input prompt but also on the information retrieved by the *retriever*.  This enhanced input structure ensures that the generated response is grounded in accurate and contextually appropriate knowledge, enhancing the overall quality of the response. Figure 1 illustrates RAG process flow. 

The synergy between the retriever and the generator in RAG leverages the strengths of both models, resulting in a more informed and contextually rich generation process. Making RAG particularly effective in tasks requiring a nuanced understanding of diverse topics, such as question answering and content creation. This innovative approach represents a significant stride forward in the field of natural language processing, addressing some of the limitations inherent in traditional generative models.

<img width="732" alt="image" src="https://github.com/maninimadireddy/NEWS_PERSONALIZATION/assets/63031546/df3d955f-f693-41b2-9756-957c381f4ae1">




***News Personalization: Leveraging RAG for Targeted Content Delivery***

To address the information overload encountered by modern news consumers, I built a tool leveraging RAG and LLMs for personalized news article retrieval and summarization. The process starts with a user entering a search request. Then RAG employs semantic search to identify relevant articles. The retrieved articles are then fed into an LLM, acting as a sophisticated summarization engine, to produce concise and accurate summaries capturing the essence across the articles. 

Getting into some technical details of this exercise I am using the Kaggle news dataset as my archived knowledge base. The first step in the process is converting the archieved news article features into vector embeddings and store in a vector database (using Pinecone). I am using Sentence-BERT(SBERT) to generate vector embeddings. SBERT is a modification of pre-trained BERT using siamese network topology along with triplet network loss to derive semantically meaningful sentence embeddings to improve sentence level semantic search. Now we have our *retriever* module; a Pinecone database populated with vectors. In this case, *retriever* takes in text queries from the user,  converts them to vectors and returns the top k relevant articles (using cosine similarity). The retriever response (list of articles) is then passed through a summarizer to generate summaries. Refer to Figure 2, for an illustration of the process flow. I have tested out a couple of different scenarios for this use case, different LLM models (all based on the same foundational T5 model) and with/without RAG context; results have been summarized in Figure 3. For more details on the code and the process flow refer to repository.

<img width="682" alt="image" src="https://github.com/maninimadireddy/NEWS_PERSONALIZATION/assets/63031546/bf3f9557-2d31-44c4-8903-5ee68db8c44a">

<img width="730" alt="image" src="https://github.com/maninimadireddy/NEWS_PERSONALIZATION/assets/63031546/587ee6fd-f255-4706-a736-147983f00754">


