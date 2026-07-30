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


This will **render as a formatted code block** in your GitHub README.

---

## ✅ Step 2: Add Your Python Code to the `README.md`

### 📄 Example: Add the `clipboard_mcp.py` code to your `README.md`

You can **embed the Python code** directly in the `README.md` — so users can **see it**, **copy it**, and **run it**.

Here’s how to do it:

### 🔧 Add This to Your `README.md` (After "Setup")

```markdown
## 🛠️ Python Code

Here’s the full `clipboard_mcp.py` script. Save it to your machine and run it.

```python
 
from fastmcp import FastMCP
import pyperclip

mcp = FastMCP("clipboard")

#!/usr/bin/env python3
from mcp.server.fastmcp import FastMCP
import subprocess

mcp = FastMCP("clipboard")

@mcp.tool()
def read_clipboard() -> str:
    """Read the current macOS clipboard text."""
    try:
        result = subprocess.run(
            ["pbpaste"],
            capture_output=True,
            text=True,
            check=True
        )
        return result.stdout
    except Exception as e:
        return f"Error reading clipboard: {e}"

@mcp.tool()
def write_clipboard(content: str) -> str:
    """Write text to the macOS clipboard."""
    try:
        subprocess.run(
            ["pbcopy"],
            input=content,
            text=True,
            check=True
        )
        return "Clipboard updated."
    except Exception as e:
        return f"Error writing clipboard: {e}"

if __name__ == "__main__":
    mcp.run(transport="stdio")

Add to mcp.json in LM Studio:

{
  "mcpServers": {
    "clipboard": {
      "command": "uv",
      "args": [
        "run",
        "--with",
        "fastmcp",
        "/Users/blakeaynes/Desktop/chat_cleaner/clipboard_mcp.py"
      ]
    }
  }
} 
