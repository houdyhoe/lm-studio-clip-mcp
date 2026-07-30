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
    print("Created by Blake Aynes")
    print("Available tools: read_clipboard, write_clipboard")
    mcp.run()

Add to mcp.json in LM Studio:


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

