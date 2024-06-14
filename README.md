# Q&A Chatbot with Langchain and Multiple Data Sources
![image](https://github.com/GayaaniD/Multidatasource_QA_bot/assets/125920863/7a93234a-d838-4ea9-aee9-ea03380bb3fe)

## Project Description
This project is about how Langchain, a library designed for LLM (Large Language Model) workflows, can be used to create a Q&A project that leverages multiple data sources. We’ll delve into the concepts of agents, tools, toolkits, and agent executors within Langchain, and how they work together

## Key Terms
  - **Tools** : Langchain offers tools as interfaces for agents, chains, or LLMs to interact with the external world. These tools can connect to various data sources like Google Search APIs, Wikipedia, or custom websites. By creating wrappers around these tools, we enable them to be integrated into our project.
  - **Toolkits** : Toolkits can group multiple tools together, allowing you to manage them as a single unit. This simplifies the process of using various data sources within your project.
  - **Agents** : While chains represent a pre-defined sequence of actions, agents leverage LLMs to make dynamic decisions about the flow of information retrieval. They utilise a prompt and LLM to determine which tools to use and in what order, based on the user’s query.
  - **Data sources** : Here we are going to use Wikipedia, Arxiv and a custom website as data sources for this RAG implementation.

## Project Flow
1. **Tools** :
Wrapping External Data Sources. Here, we’ll create tools for Wikipedia, a custom website, and Arxiv:
    - **Wikipedia Tool** : The Wikipedia tool in this project is designed to fetch and process information from Wikipedia. It is built using the `WikipediaQueryRun` class from the `langchain_community.tools` module and the `WikipediaAPIWrapper` class from the `langchain_community.utilities` module.
Here's a brief overview of how it works:
      1. **WikipediaAPIWrapper** : This class is responsible for handling the Wikipedia API. It is initialized with two parameters:
          - `top_k_results` : This parameter determines the maximum number of search results to return from a Wikipedia query.
          - `doc_content_chars_max` : This parameter sets the maximum character limit for the content of a Wikipedia document.
      
      2. **WikipediaQueryRun** : This class uses the `WikipediaAPIWrapper` to run queries on Wikipedia. It is initialized with the `api_wrapper` parameter, which is an instance of the `WikipediaAPIWrapper` class.

    - **Custom Website Tool (LangSmith Docs)** : The Custom Website Tool is designed to fetch and process information from a specific website, in this case, the LangSmith Docs. It uses several classes from the `langchain_community` and `langchain_openai` modules.
Here's a brief overview of how it works:
      1. **WebBaseLoader**: This class is responsible for loading documents from a specific website. It is initialized with the URL of the website.
      
      2. **RecursiveCharacterTextSplitter**: This class splits the loaded documents into chunks based on the specified chunk size and overlap.
      
      3. **FAISS**: This class creates a vector database from the split documents using the OpenAIEmbeddings.
      
      4. **create_retriever_tool**: This function creates a retriever tool from the vector database.
         
    - **Arxiv Tool** : The Arxiv Tool is designed to fetch and process information from the Arxiv database. It uses the `ArxivQueryRun` class from the `langchain_community.tools` module and the `ArxivAPIWrapper` class from the `langchain_community.utilities` module.
Here's a brief overview of how it works:
      1. **ArxivAPIWrapper**: This class is responsible for handling the Arxiv API. It is initialized with two parameters:
          - `top_k_results`: This parameter determines the maximum number of search results to return from an Arxiv query.
          - `doc_content_chars_max`: This parameter sets the maximum character limit for the content of an Arxiv document.
      
      2. **ArxivQueryRun**: This class uses the `ArxivAPIWrapper` to run queries on Arxiv. It is initialized with the `api_wrapper` parameter, which is an instance of the `ArxivAPIWrapper` class.
      

2. **Combining Tools and Creating the Agent**:
  This code combines the created tools into a list and utilises the create_openai_tools_agent function to create an agent. This agent employs the LLM and the pre-built prompt from Langchain Hub to decide which tool to use for each query.

4. **Executing the Agent with Agent Executor**
   
5. **Agent Execution and Response Flow**
   **The agent_executor.invoke method takes a dictionary as input, where the key “input” represents the user’s question. Here’s what happens when you execute a query**:
    - **Agent Takes Over** : The agent receives the user’s query.
    - **Decision Making with LLM** : The agent, using the LLM and the pre-defined prompt, determines the most suitable tool to address the query based on its understanding.
    - **Tool Selection and Retrieval** : The agent selects the chosen tool (e.g., Wikipedia, custom website retriever, or Arxiv) and interacts with it.
    - **Information Gathering** : The selected tool retrieves relevant information from its respective data source based on the user’s query.
    - **Response Generation** : The retrieved information is then processed and potentially combined with knowledge from other tools (depending on the prompt design), ultimately leading to a response for the user.
    - **User Receives Answer** : The agent executor presents the generated response to the user.

## How to Run the Project
1. Clone the GitHub repository.
2. Rename the `.env.example` file to `.env` and add your API keys.
3. Install the project dependencies by running the `requirements.txt` file. You can do this by opening your terminal and typing:
    ```
    pip install -r requirements.txt
    ```
4. After the dependencies are installed, you can run the project.
