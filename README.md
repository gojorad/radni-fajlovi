from pathlib import Path

root = Path(".")
exclude = {".git", "__pycache__", ".venv", "node_modules"}

files = []
for p in root.rglob("*"):
    if p.is_file() and not any(part in exclude for part in p.parts):
        if p.name.lower() != "readme.md":
            files.append(p.as_posix())

files.sort()

content = "# Project Name\n\n## Sadržaj foldera\n\n"
for f in files:
    content += f"- `{f}`\n"

content += "\n## Opis\n\nKratak opis projekta.\n"

Path("README.md").write_text(content, encoding="utf-8")
print("README.md napravljen.")
