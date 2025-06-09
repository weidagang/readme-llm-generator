# README.llm Generator 🤖

This tool generates a `README.llm` file for a given source code repository. The generated file provides a machine-readable summary of the codebase, which can be used to give Large Language Models (LLMs) better context, improving the quality of their generated code.

The tool is packaged as a Docker image for portability and ease of use.

## ✨ Features

-   Analyzes source code repositories to create a high-level summary.
-   Uses the Gemini API for code analysis.
-   Configurable to scan for specific file types (e.g., `.py`, `.ts`, `.java`).
-   Generates language-specific output formats (e.g., Python `.pyi`, TypeScript `.d.ts`, Java `interface`).

## 📋 Requirements

-   Docker
-   Bash (for running helper scripts)

## 🚀 Getting Started

### 1. **Clone the Project**

First, get the project files on your local machine.

```bash
git clone <your-repository-url>
cd readme-llm-generator
```

### 2. Configuration
The tool requires a Google API key to interact with the Gemini API. Configuration is loaded from a .env file.

Create a .env file by copying the example:

```
cp .env.example .env
```

Edit the .env file and add your credentials:

```bash
# .env
GOOGLE_API_KEY=YOUR_API_KEY
GEMINI_MODEL=gemini-2.0-flash
```

### 3. Build the Docker Image

A helper script is provided to build the Docker image.

First, make the script executable:

```bash
chmod +x scripts/create-image.sh
```

Then, run the script:

```bash
./scripts/create-image.sh
```

### 4. Run the Generator

Another helper script simplifies generating the README.llm.

Make the script executable:

```bash
chmod +x scripts/generate-readme-llm.sh
```

Run the script, passing the path to the repository you want to analyze:

```bash
./scripts/generate-readme-llm.sh /path/to/your/repo
```

The output file, README.llm, will appear in the root of your target project directory (/path/to/your/repo).

Manual Docker Commands (Alternative)
If you prefer not to use the scripts, you can run the Docker commands manually:

Build:

```bash
docker build -t readme-llm-generator .
```

Run:

```bash
docker run --rm --env-file ./.env -v /path/to/your/repo:/app/repo readme-llm-generator
```