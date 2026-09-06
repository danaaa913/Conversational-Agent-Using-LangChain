# PDF Context Retrieval Agent

A notebook prototype for uploading PDFs, retrieving relevant passages and recording conversation history, using LangChain, ChromaDB, SentenceTransformers and LangGraph.

## Explore the implementation

[Untitled23.ipynb](Untitled23.ipynb) contains several iterations: FastAPI upload/search endpoints, a graph-based API, and a final Gradio interface with PDF upload, questions and history tabs.

The final graph runs **retrieve → generate → save history**. The node named `generate` joins retrieved text passages; it does not call an LLM. The notebook does not implement the ReAct tool-selection behavior described in the original repository description.

## Run the Gradio experiment

1. Open the notebook in a fresh Google Colab runtime.
2. Install the dependencies used by the Gradio section: `gradio chromadb pypdf langgraph langchain langchain-community langchain-huggingface sentence-transformers`.
3. Run the self-contained Gradio cell beginning with its package-install command and `VECTORDB = "gradio_db_clean"`. Earlier API server cells are separate experiments and do not need to be run first.
4. Upload a text-based PDF, ask a question, and inspect the returned excerpts and saved history.

The existing `app.launch(share=True)` requests a temporary public link. The Gradio cell resets its local `gradio_db_clean` directory when rerun. Use a disposable runtime and sample documents.

## API variants and limitations

Earlier cells use FastAPI/Uvicorn and optional ngrok tunnels. They include alternate request schemas and ports; inspect the selected server's `/docs` instead of mixing requests across versions.

- The Gradio demo uses one hardcoded session ID and a shared document store.
- History is recorded, but retrieval is based on the current question.
- Text extraction does not include OCR for scanned PDFs.
- Legacy LangChain imports and Gradio file handling may need version-specific updates. Dependencies are not pinned and end-to-end compatibility has not been established.
