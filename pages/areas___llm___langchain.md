- Two principles
	- *Data-aware*: connect a language model to other sources of data
	- *Agentic*: allow a language model to interact with its environment
- langfuse:
- Modules
	- Schema
		- Text
		- ChatMessages
		- Examples: input/output pairs that represent inputs to a function and then expected output. They can be used in both training and evaluation of models.
		- Document: A piece of unstructured data. Consists of `page_content` (the content of the data) and `metadata` (auxiliary pieces of information describing attributes of the data).
	- Model
	  collapsed:: true
		- llm: take a text string as input, and return a text string as output.
		- ChatModel: take a list of Chat Messages as input, and return a Chat Message.
		- **Text Embedding Models**: take text as input and return a list of floats.
	- Prompts
	  collapsed:: true
		- PromptValue: The class representing an input to a model.
		- **Prompt Templates**: The class in charge of constructing a PromptValue.
		- Example selector:
		- output parser: responsible for
			- (1) instructing the model how output should be formatted,
			- (2) parsing output into the desired formatting (including retrying if necessary).
	- Indexes: ways to structure documents so that LLMs can best interact with them
	  collapsed:: true
	  :LOGBOOK:
	  CLOCK: [2023-06-11 Sun 10:24:32]
	  :END:
		- Document Loaders: responsible for loading documents from various sources
		- Text Splitters: splitting text into smaller chunks
		- VectorStores
		- Retrievers: Interface for fetching relevant documents to combine with language models.
	- Memory
	  collapsed:: true
		- short, long
		- ChatMessageHistory: `add_user_message`, `add_ai_message`, `messages`
	- Chains: returns to a sequence of modular components (or other chains) combined in a particular way to accomplish a common use case
	  collapsed:: true
		- LLMChain
		- Index-related chains: combine your own data (stored in the indexes) with LLMs. The best example of this is question answering over your own documents
			- Stuffing
			- Map Reduce
			- Refine
			- Map-rerank
		- PromptSelector: responsible for choosing a default prompt depending on the model passed in
	- Agents: has access to a suite of **tools**. Depending on the user input, the agent can then decide which, if any, of these tools to call.
		- **Action Agents**
		- **Plan-and-Execute Agents**
	- Callbacks
		- *Constructor callbacks*
		- *Request callbacks*
- Use Cases
	- [Autonomous Agents](https://python.langchain.com/en/latest/use_cases/autonomous_agents.html#)
	- [Agent Simulations](https://python.langchain.com/en/latest/use_cases/agent_simulations.html)
	- [Agents](https://python.langchain.com/en/latest/use_cases/personal_assistants.html)
	- [Question Answering over Docs](https://python.langchain.com/en/latest/use_cases/question_answering.html)
	- [Chatbots](https://python.langchain.com/en/latest/use_cases/chatbots.html)
	- [Personal Assistants](https://docs.langchain.com/docs/use-cases/personal-assistants)
	- [Querying Tabular Data](https://docs.langchain.com/docs/use-cases/qa-tabular)
	- [Code Understanding](https://python.langchain.com/en/latest/use_cases/code.html#)
	- [Interacting with APIs](https://docs.langchain.com/docs/use-cases/apis)
	- [Extraction](https://docs.langchain.com/docs/use-cases/extraction)
	- [Evaluation](https://docs.langchain.com/docs/use-cases/evaluation)
	- [Summarization](https://docs.langchain.com/docs/use-cases/summarization)
- misc
	- Modular Reasoning, Knowledge and Language (MRKL): **neuro-symbolic architecture** that combine LLMs (neural computation) and external tools like calculators (symbolic computation), to solve complex problems.
	- retrieval augmented generation (RAG)