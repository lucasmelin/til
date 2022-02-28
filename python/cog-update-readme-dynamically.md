# Using cog to update my TILs in a Markdown README file

As I add new TILs to this repo, I wanted a way to easily update the README without having to remember to update _two_ files every time (the TIL and the README).

I'd recently read [Simon Willison's TIL](https://github.com/simonw/til/blob/main/python/cog-to-update-help-in-readme.md) about doing something similar using [cog](https://nedbatchelder.com/code/cog), so I decided to try using that.

Here's what I came up with:

```markdown
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
<!---[[[end]]]-->
```

Then to update the README file in-place, I can run `cog  -r README.md`

Since GitHub Actions usage is currently [free for public repositories](https://docs.github.com/en/billing/managing-billing-for-github-actions/about-billing-for-github-actions#about-billing-for-github-actions), I've also setup an [Actions workflow](../.github/workflows/update-readme.yaml) to automatically update the README whenever a new commit is made to the `main` branch.