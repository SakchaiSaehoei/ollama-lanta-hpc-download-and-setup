
---


# 🧠 Running Ollama on LANTA HPC (Transfer Node)

This guide walks you through setting up [Ollama](https://ollama.com) for large language model inference on a LANTA HPC transfer node, with a custom port and model path setup.

---

## 📦 1. Environment Setup

### ⬇️ Download and Extract Ollama

```bash
# Login to the LANTA transfer node
mkdir ollama && cd ollama

# Download the Ollama binary for Linux
curl -L https://ollama.com/download/ollama-linux-amd64.tgz -o ollama-linux-amd64.tgz

# Extract the archive
tar -xvf ollama-linux-amd64.tgz

# Create directory to store models
mkdir models
```

---

## ⚙️ 2. Environment Variables

```bash
# Add Ollama libraries to the dynamic linker path
export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:$(pwd)/lib

# Add Ollama binary to your PATH
export PATH=${PATH}:$(pwd)/bin

# Set the path to store downloaded models
export OLLAMA_MODELS=$(pwd)/models

# Set a custom host and port for the Ollama server
export OLLAMA_HOST=127.0.0.1:12345
```

> ✅ Tip: Add these exports to your `.bashrc` or `.bash_profile` to persist across sessions.

---

## 🚀 3. Start Ollama Server

```bash
ollama serve &
```

This will launch the Ollama backend server in the background on port `12345`.

---

## 🧠 4. Pull and Run a Model

### 📥 Pull the LLaMA3 8B model

```bash
ollama pull llama3:8b
```

### ▶️ Run the model

```bash
ollama run llama3:8b
```

### 📋 List available models

```bash
ollama list
```

---

## 🛑 Stopping the Ollama Server

If you started the server with `&`, find its process:

```bash
ps aux | grep ollama
```

Then stop it with:

```bash
kill <PID>
```

If it doesn't stop:

```bash
kill -9 <PID>
```

---

## 📁 Project Directory Structure

```
ollama/
├── bin/                   # Ollama binaries
├── lib/                   # Ollama libraries
├── models/                # Local model storage
├── ollama-linux-amd64.tgz
├── setup_ollama.sh        # Optional: install script
├── ollama_environment_setup.sh  # Optional: generated env script
└── README.md
```

---

## 📚 References

* [Ollama Official Site](https://ollama.com)

---

## ✅ Author

Maintained by **Sakchai Saehoei**

```

```
