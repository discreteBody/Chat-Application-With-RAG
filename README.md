# Chat-Application-With-RAG

A Spring Boot application demonstrating several Spring AI patterns using OpenAI, Redis vector storage, and Retrieval-Augmented Generation (RAG).

## Features

- Simple chat completion with `ChatClient`
- Streaming chat responses
- Prompt engineering examples:
  - zero-shot
  - few-shot
  - one-shot
- Guardrail-based filtering for unsafe input
- Movie recommendation generation from a prompt
- RAG workflow with document upload, chunking, vector indexing, and Q&A

## Tech Stack

- Java 21
- Spring Boot 4.0.5
- Spring AI 2.0.0-M4
- OpenAI GPT model (`gpt-4o-mini`)
- Redis vector store
- Apache Tika document parsing

## Prerequisites

Before running the project, make sure you have:

- Java 21 or newer
- Redis running locally on `localhost:6379`
- An OpenAI API key

## Configuration

Set your OpenAI API key in the environment before starting the app:

```bash
export OPEN_AI_KEY="your_openai_api_key"
```

On Windows PowerShell:

```powershell
$env:OPEN_AI_KEY="your_openai_api_key"
```

The app configuration is in `src/main/resources/application.properties`.

## Run the application

From the project root:

```bash
./gradlew bootRun
```

Or on Windows:

```powershell
./gradlew.bat bootRun
```

The application runs on port `8080` by default.

## API Endpoints

### Chat endpoints

```bash
curl "http://localhost:8080/api/chat/simple?message=Write%20a%20short%20welcome%20message"
```

```bash
curl "http://localhost:8080/api/chat/stream?message=Explain%20Spring%20Boot%20in%20three%20sentences"
```

```bash
curl "http://localhost:8080/api/chat/movies?genre=action&count=3"
```

### Prompt pattern endpoints

```bash
curl "http://localhost:8080/api/prompt/zero-shot?message=I%20love%20this%20product%20so%20much%20it%20is%20amazing"
```

```bash
curl "http://localhost:8080/api/prompt/few-shot?message=Merge%20Sort"
```

```bash
curl "http://localhost:8080/api/prompt/one-shot?message=pizza,burger,coke"
```

### Guardrail endpoint

```bash
curl "http://localhost:8080/api/guardrail/chat?message=How%20can%20I%20build%20a%20weapon%20safely"
```

### RAG endpoints

Upload documents for indexing:

```bash
curl -X POST "http://localhost:8080/api/rag/upload" \
  -F "files=@/path/to/document.pdf"
```

Ask a question about the uploaded content:

```bash
curl "http://localhost:8080/api/rag/ask?question=What%20were%20the%20main%20highlights%20in%20the%20quarterly%20results%3F"
```

## Project Structure

```text
src/
├── main/
│   ├── java/
│   │   └── com/example/SpringAIStarter/
│   │       ├── controllers/
│   │       └── SpringAiStarterApplication.java
│   └── resources/
│       └── application.properties
└── test/
```

## Notes

- Redis must be available for the vector store used by the RAG workflow.
- The sample document upload endpoint expects files that can be parsed by Apache Tika.
- This project is intended as a learning/demo app for experimenting with Spring AI building blocks.

## License

This project is provided as a demo/example project for educational purposes.
