- **unifies the sophistication of Microsoft Azure Bot Framework Composer’s pro-code capabilities with the simplicity of Power Virtual Agents’ low-code platform**: Power Virtual Agents studio.
- Environments represent space to store, manage, and share your organization's business data. Each bot that you create is stored in an environment.
	- might have different roles, security requirements, and target audiences
	- Individual environments are not created in Power Virtual Agents; they are created in a separate location
	- default environment
	- added extra environments through the [Microsoft Power Platform admin center](https://learn.microsoft.com/en-us/power-platform/admin/create-environment/).
	- **Create a database for this environment**: for dataverse
- **Topics** define how the customers will interact with the bot, and they typically represent common issues, questions, or tasks that customers might need assistance with.
	- consists of two primary elements
		- **Trigger phrases**: Phrases, keywords, or questions that are entered by users and relate to a specific issue.
		- **Conversation nodes** : Define how a bot should respond and what it should do.
	- predefined topics
		- **Lesson** - Pre-created user topics that can help you understand simple and complex ways of using nodes to create bot conversations.
		- **System** - represent scenarios that customers are likely to encounter while interacting with your bot, such as initiating and ending a conversation or escalating a conversation to a live agent. System topics will have a basic structure already in place, based on what the scenario is
			-
- conversation booster
- Azure OpenAI on your data
- [Information Sources](https://learn.microsoft.com/en-us/power-virtual-agents/nlu-boost-node#information-sources)
	- file types:
		- SharePoint pages (aspx pages)
		- Word documents (docx)
		- PowerPoint documents (pptx)
		- PDF documents (pdf)
	- <table aria-label="Table 1" class="table table-sm">
	  <thead>
	  <tr>
	  <th>Name</th>
	  <th>Source</th>
	  <th>Description</th>
	  <th>Number of Inputs</th>
	  <th>Authentication</th>
	  </tr>
	  </thead>
	  <tbody>
	  <tr>
	  <td>Bing Search</td>
	  <td>External</td>
	  <td>Searches the query input on Bing; returning results only from provided websites</td>
	  <td>4 public URLs (for example, <em>microsoft.com</em>)</td>
	  <td>None</td>
	  </tr>
	  <tr>
	  <td>Bing Custom Search</td>
	  <td>External</td>
	  <td>Query input filtered based on a website configuration external to Power Virtual Agents</td>
	  <td>Each search ID can use more than 4 URLs (Bing Custom Search also provides other functionality) but you can only connect to one search ID</td>
	  <td>None</td>
	  </tr>
	  <tr>
	  <td>Azure OpenAI on your data</td>
	  <td>Internal</td>
	  <td></td>
	  <td>Defined by your Azure OpenAI Service connection</td>
	  <td>Bot user's Azure Active Directory (Azure AD) authentication</td>
	  </tr>
	  <tr>
	  <td>Documents</td>
	  <td>Internal</td>
	  <td>Searches documents uploaded to Dataverse, returning results from the document contents</td>
	  <td>Limited by Dataverse file storage allocation</td>
	  <td>None</td>
	  </tr>
	  <tr>
	  <td>SharePoint</td>
	  <td>Internal</td>
	  <td>Connects to a SharePoint URL, uses GraphSearch to return results</td>
	  <td>4 URLs</td>
	  <td>Bot user's Azure Active Directory (Azure AD) authentication</td>
	  </tr>
	  <tr>
	  <td>OneDrive for Business</td>
	  <td>Internal</td>
	  <td>Connects to a OneDrive for Business URL, uses GraphSearch to return results</td>
	  <td>4 URLs</td>
	  <td>Bot user's Azure Active Directory (Azure AD) authentication</td>
	  </tr>
	  <tr>
	  <td>Custom data</td>
	  <td>Internal</td>
	  <td>Uses a JSON code block to define the URLs and content to use</td>
	  <td>One variable, populated with the JSON results to be summarized</td>
	  <td>Dependent on source</td>
	  </tr>
	  </tbody>
	  </table>
- Copilot in Power Virtual Agents
- Use uploaded documents for generative answers
	- Contents of the files you upload will be available to all users.
	- [Supported document types](https://learn.microsoft.com/en-us/power-virtual-agents/nlu-documents#supported-document-types)
	  collapsed:: true
		- Word documents (doc, docx)
		- Excel spreadsheets (xls, xlsx)
		- PowerPoint documents (ppt, pptx)
		- PDF documents (pdf)
		- Text documents (.txt, .md, .log)
		- HTML files (html, htm)
		- CSV files (csv)
		- XML files (xml)
		- OpenDocument files (odt, ods, odp)
		- EPUB documents (epub)
		- Rich Text Format documents (rtf)
		- Apple iWork documents (pages, key, numbers)
		- JSON files (json)
		- YAML files (yml, yaml)
		- LaTeX files (tex)