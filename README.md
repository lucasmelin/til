# Today I Learned

My Today I Learned snippets. Inspired by [jbranchaud/til](https://github.com/jbranchaud/til) and  [simonw/til](https://github.com/simonw/til).

<!---[[[cog
import cog
from pathlib import Path

project_dir = Path.cwd()

topics = [x for x in project_dir.iterdir() if x.is_dir() and not x.name.startswith(".")]
md_count = len(list(project_dir.glob("**/*.md")))
til_count = md_count - 1 # README
cog.outl(f"{til_count} TILs so far.")
for topic in topics:
    cog.outl(f"## {topic.name}")
    tils = topic.glob("**/*.md")
    for til in tils:
        with til.open('r') as f:
            title = f.readline().replace("# ", "")
        cog.outl(f"- [{title}]({til.relative_to(project_dir)})")
    cog.outl()
]]]-->
2 TILs so far.
## playwright
- [In working with [Playwright](https://playwright.dev/), sometimes you need to search for an element like a button or dropdown that might have one of several attributes.
](playwright/multiple-condition-selector.md)

## python
- [Using cog to update my TILs in a Markdown README file
](python/cog-update-readme-dynamically.md)

<!---[[[end]]]-->