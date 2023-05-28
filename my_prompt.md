write an HTML file with the below python code chunk inserted using py-script, structure the html like the following:

```html
<html>
<head>
    <link rel="stylesheet" href="https://pyscript.net/alpha/pyscript.css" />
    <script defer src="https://pyscript.net/alpha/pyscript.js"></script>
</head>
<body>
    <py-script>
        insert python code chunk here
    </py-script>
</body>
</html>
```

Use the below python code chunk and Wrap the output of the print statement in css using the CSS bootstrap framework:

```python
import os
import langchain
from langchain.document_loaders import PyPDFLoader 
from langchain.embeddings import OpenAIEmbeddings 
from langchain.vectorstores import Chroma 
from langchain.chains import ConversationalRetrievalChain
from langchain.memory import ConversationBufferMemory
from langchain.llms import OpenAI

# use python-dotenv to get API key
from dotenv import load_dotenv
load_dotenv()

os.environ.get("OPENAI_API_KEY")



# load whitepaper (already saved in directory) to langchain
pdf_path = "../curve-stablecoin.pdf" 
loader = PyPDFLoader(pdf_path)
pages = loader.load_and_split()


# creating embeddings and vectorization
embeddings = OpenAIEmbeddings()
vectordb = Chroma.from_documents(pages, embedding=embeddings, persist_directory=".")
vectordb.persist()
memory = ConversationBufferMemory(memory_key="chat_history", return_messages=True)
pdf_qa = ConversationalRetrievalChain.from_llm(OpenAI(temperature=0.8), vectordb.as_retriever(), memory=memory)

# query
query = "What is Curve Stablecoin?"
result = pdf_qa({"question": query})
print(query)
print("Answer:")
result["answer"]
print(result["answer"])
```

## debugging notes

import langchain, when giving the following error:

```js
JsException(PythonError: Traceback (most recent call last): File "/lib/python3.10/site-packages/_pyodide/_base.py", line 429, in eval_code .run(globals, locals) File "/lib/python3.10/site-packages/_pyodide/_base.py", line 300, in run coroutine = eval(self.code, globals, locals) File "", line 4, in ModuleNotFoundError: No module named 'langchain' )
```

if the error persist, do the following:

```python
from platform import python_version
print(python_version())
```

make sure python 3.10.11 is installed