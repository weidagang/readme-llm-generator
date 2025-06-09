# README.llm Generator 🤖

This tool generates a `README.llm` file for a given source code repository. The generated file provides a machine-readable summary of the codebase, which can be used to give Large Language Models (LLMs) better context, improving the quality of their generated code.

The tool is packaged as a Docker image for portability and ease of use.

## ✨ Features

-   Analyzes source code repositories to create a high-level summary.
-   Leverages the Gemini API and its large context window for code analysis.
-   Configurable to scan for specific file types (e.g., `.py`, `.ts`, `.java`).
-   Generates language-specific output formats (e.g., Python `.pyi`, TypeScript `.d.ts`, Java `interface`).

## ⚙️ How It Works

The tool follows a simple workflow to analyze your code and generate README.llm:

1.  **Code Parsing**: The Python script starts and recursively scans the `/app/repo` directory, finding all source files that match the configured extensions (e.g., `.py`, `.go`). The contents of all found files are read and concatenated into a single text block.
2.  **Prompt Construction**: The script reads the `system_prompt.md` template and appends the aggregated source code, creating a complete and detailed prompt for the AI.
3.  **Gemini API Call**: This final prompt is sent to the Gemini API for analysis.
4.  **Output Generation**: The tool receives the generated summary from the API and writes it to a new file named `README.llm`.

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