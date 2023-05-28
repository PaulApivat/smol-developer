create python script and save to new file called query_pdf.py, that imports the following methods from langchain:

```python
from langchain.document_loaders import PyPDFLoader 
from langchain.embeddings import OpenAIEmbeddings 
from langchain.vectorstores import Chroma 
from langchain.chains import ConversationalRetrievalChain
from langchain.memory import ConversationBufferMemory
from langchain.llms import OpenAI
```

- create python environment variable to grab OPENAI_API_KEY in the script
- without replacing the current file, use methods provided by langchain to load and read the curve-stablecoin.pdf file in the current directory (do not replace)
- create embeddings 
- store in a vectorstore
- ensure vectordb persists in memory
- ask a question to OpenAI llms to summarize the paper
- print response from llms

