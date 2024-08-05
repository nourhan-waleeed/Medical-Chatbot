# Medical-Chatbot

Here I utilized a Retrieval-Augmented Generation (RAG) system enhanced with a Generative Feedback Loop (GFL) to improve document retrieval and response generation in Chatbot.



Key Components:

1- Document Processing:

 I leveraged LangChain open source framework to load and split a PDF document into chunks.

These chunks are then embedded using Google's Generative AI model (Gemini).



 2-Database Integration:

The embedded chunks are stored in a ClickHouse database for quick retrieval (MYScaleDB).

 

3- RAG System:

When a user asks a question, we find the most relevant document chunks using vector similarity search within the database.

These relevant chunks are used to create a context-aware prompt for the Gemini Pro model.



For more efficiency I've added an Agent performing Generative Feedback Loops (GFL) to The Retrieval Augmented Generation (RAG) pipeline to boost speed and reduce costs.



GFL save LLM-generated results to the database, expanding the chatbot's knowledge base and improving query handling. This approach reduces costs by using cached results for similar queries.



For Simplicity: 

When a user asks a question, we search past question/answer pairs for similar ones. 

 If no similar question exists, we use an expensive model to generate a response with vector database context in my case I used Gemini.

 If similar questions exist, we use a cheaper, smaller model to adjust the response for this I used flan-t5-small.

 
ex: here when the question was first asked it was passed to the expensive model but in the second query a similar question was asked so the cheap model modified the answer so it took less time to adjust than to generate
![image](https://github.com/user-attachments/assets/fab1dfed-267b-4b6e-8904-f3d511037f8a)
