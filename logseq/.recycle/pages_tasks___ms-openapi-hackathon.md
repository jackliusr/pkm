- repository: https://dev.azure.com/sntuc/_git/TO%20Tech%20Playground
- MSDN setups
- prerequisite:
- TO Tech Playground repo -> MS-Hackathon-202311 -> reference
- [Hackathon Briefing.pptx](https://sntuc.sharepoint.com/:p:/r/sites/TODataandTechnology/Shared%20Documents/TA%20Collaboration/Microsoft%20Hackathon%202023/Hackathon%20Briefing.pptx?d=wfaac7bbac75e478cb035e823b466149f&csf=1&web=1&e=IHF69c)
- ``` powershell
  conda install pyyaml azure-core azure-storage-blob numpy pandas openpyxl nltk openai gensim scikit-learn scikit-learn-intelex jupyterlab black isort flake8 ipywidgets fsspec validators streamlit streamlit-chat
   
  pip install azure-ai-formrecognizer azure-search-documents tiktoken azure-identity azure-keyvault-secrets langchain azure-data-tables streamlit-authenticator
  ```
- [SSL: certificate_verify_failed](https://community.openai.com/t/ssl-certificate-verify-failed/32442/62?page=2)
- chat
	- GUI
		- Using Power Virtual Agents
		- Using the web app: https://github.com/microsoft/sample-app-aoai-chatGPT
	- Chat history
	- Through the system prompt and [prompt engineering](https://learn.microsoft.com/en-us/azure/cognitive-services/openai/concepts/prompt-engineering), you can also feed the model with instructions, rules and input data before it generates an answer.
	- **Power Virtual Agents capabilities and features are now part of Microsoft Copilot Studio** following significant investments in generative AI and enhanced integrations across Microsoft Copilot. Some articles and screenshots may refer to Power Virtual Agents while we update documentation and training content.
	- ![](https://techcommunity.microsoft.com/t5/image/serverpage/image-id/489223iF8F8CB0370773E6D/image-dimensions/972x531?v=v2)
	- [ChatGPT + Enterprise data with Azure OpenAI and AI Search](https://github.com/Azure-Samples/azure-search-openai-demo/)
	- Azure Bot Service channels