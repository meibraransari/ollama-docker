# Ollamam Integration config with Continue extension

## 📋 Configuration path on windows
- C:\Users\<YOUR_USER>\.continue\config.yaml

## Config

```bash
name: Remote
version: 1.0.0
schema: v1
models:
  - name: Lllama 3.1 7B
    provider: ollama
    model: llama3.2:3b
    #model: gemma3:12b
    #model: deepseek-r1:14b
    env:
      useLegacyCompletionsEndpoint: false
    baseUrl: http://192.168.1.100:11434
    apiBase: http://192.168.1.100:11434
    num_ctx: 16384
    # "parameters": {
    #     "num_ctx": 1024
    #   }
    roles:
      - chat         # For conversational interfaces
      - edit         # For editing or refactoring code
      - apply        # For applying changes or suggestions
      - autocomplete # For code or text autocompletion
      #- completion   # For generic text/code completion
      #- code         # If used for coding-specific features (varies by system)
      #- assistant    # General assistant-type tasks
      #- debug       # Example: Adding a role for debugging assistance
context:
  - provider: code
  - provider: docs
  - provider: diff
  - provider: terminal
  - provider: problems
  - provider: folder
  - provider: file
  - provider: codebase
  - provider: currentFile
  - provider: search
  - provider: open
  #   params:
  #     onlyPinned: true
  # - provider: web
  #   params:
  #     n: 5

---
### 💼 Connect with me 👇👇 😊

- 🔥 [**Youtube**](https://www.youtube.com/@DevOpsinAction?sub_confirmation=1)
- ✍ [**Blog**](https://ibraransari.blogspot.com/)
- 💼 [**LinkedIn**](https://www.linkedin.com/in/ansariibrar/)
- 👨‍💻 [**Github**](https://github.com/meibraransari?tab=repositories)
- 💬 [**Telegram**](https://t.me/DevOpsinActionTelegram)
- 🐳 [**Docker**](https://hub.docker.com/u/ibraransaridocker)
