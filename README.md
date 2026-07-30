I’ve built **ClipMCP** — a lightweight tool to reduce context bloat in LM Studio.

Local LLMs are powerful — but long conversations fill context, increase VRAM usage, and shorten session length.

That’s why I built **ClipMCP** — a small Python server that lets LM Studio models access your system clipboard — securely and locally.

✅ Read clipboard content on-demand  
✅ Write output to clipboard  
✅ No context bloat  
✅ No cloud, no token waste  
✅ Full control — you decide what’s shared

### How it works:
1. Run `clipboard_mcp.py` (uses `fastmcp` and `pyperclip`)
2. Add to `mcp.json` in LM Studio
3. Call `read_clipboard()` or `write_clipboard()` from the model

### Example:
> “Read the current clipboard content and help me analyze it.”

Then paste a function — no context bloat.

### Why this matters:
- Reduces unnecessary tokens
- Lowers memory pressure
- Extends session length
- Keeps you inside LM Studio

I built this to solve my own workflow problem — and now I’m sharing it.
  Made by **Blake Aynes** — a tool to help local LLMs work smarter, not harder.
  Feedback? Issues? Let me know!


 ```python
# Your Python code here
print("Hello, world!")


# ClipMCP

A lightweight MCP server that gives LM Studio models controlled access to the system clipboard.

Local LLMs are powerful — but long conversations fill the context window, increase VRAM usage, and shorten useful session length.

**ClipMCP** solves this by letting models read from and write to the clipboard on demand, while keeping you inside LM Studio’s native chat interface.

## Features

- Read clipboard content on demand
- Write text to the clipboard
- No cloud dependency
- Reduces unnecessary tokens in context
- Lowers memory and VRAM pressure
- Extends usable session length
- Works with vision models and other MCPs

## How it works

1. Run the `clipboard_mcp.py` server
2. Add it to your `mcp.json` in LM Studio
3. Ask the model to read or write to the clipboard

### Example prompts

> Read the current clipboard content and help me analyze it.

> Write a summary of this conversation to my clipboard.

## Setup

### 1. Create the script

Save the following as `clipboard_mcp.py`:

```python
#!/usr/bin/env python3
from fastmcp import FastMCP
import pyperclip

mcp = FastMCP("clipboard")

@mcp.tool()
def read_clipboard() -> str:
    """Read the current text content from the system clipboard."""
    try:
        content = pyperclip.paste()
        return content if content else "(clipboard is empty)"
    except Exception as e:
        return f"Error reading clipboard: {e}"

@mcp.tool()
def write_clipboard(text: str) -> str:
    """Write the given text to the system clipboard."""
    try:
        pyperclip.copy(text)
        return "Successfully wrote text to the clipboard."
    except Exception as e:
        return f"Error writing to clipboard: {e}"

if __name__ == "__main__":
    print("Clipboard MCP server starting...")
    print("Available tools: read_clipboard, write_clipboard")
    mcp.run(

2. Install dependencies

python3 -m pip install fastmcp pyperclip

3. Add to LM Studio
Add this entry to your mcp.json:

{
  "mcpServers": {
    "clipboard": {
      "command": "python3",
      "args": [
        "/path/to/your/clipboard_mcp.py"
      ]
    }
  }
}

4. Start the server

python3 clipboard_mcp.py

