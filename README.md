# Rate My Professor RAG Assistant

A chat assistant that recommends professors using retrieval-augmented generation (RAG). Ask something like "Who is the best professor for intro physics?" and it retrieves the most relevant student reviews from a vector database, then answers with the top three matches.

**Live site:** https://rate-my-professor-pink.vercel.app

## How it works

1. **Indexing** (`load.ipynb`): each review in `reviews.json` is embedded with OpenAI `text-embedding-3-small` and upserted into a **Pinecone** index named `rag` (namespace `ns1`), with the professor, subject, review text, and star rating as metadata.
2. **Retrieval** (`app/api/chat/route.js`): the user's question is embedded with the same model and used to query Pinecone for the top 3 matches.
3. **Generation:** the matches are added to the prompt and sent to `gpt-4o-mini`, and the answer streams back to the chat UI.

## Tech stack

| Layer | Tools |
|---|---|
| Frontend | Next.js 14, React, Material UI |
| Embeddings and chat | OpenAI API (`text-embedding-3-small`, `gpt-4o-mini`) |
| Vector database | Pinecone |
| Indexing | Python, Jupyter |
| Hosting | Vercel |

## Run locally

```bash
git clone https://github.com/Amm1el/Rate-My-Professor-RAG.git
cd Rate-My-Professor-RAG
npm install
npm run dev
```

Create `.env.local` with:

| Variable | Description |
|---|---|
| `OPENAI_API_KEY` | OpenAI API key |
| `PINECONE_API_KEY` | Pinecone API key |

To build the index, run `load.ipynb` with the same keys in a `.env` file. The sample dataset in `reviews.json` contains 7 reviews; replace it with your own data to extend the assistant.

## Author

Ammiel Bowen · [ammielbowen.com](https://ammielbowen.com) · [LinkedIn](https://www.linkedin.com/in/ammielbowen/)
