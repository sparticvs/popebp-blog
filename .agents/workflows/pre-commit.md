---
description: Run blog post optimization before a commit
---
Before you commit any changes, check if there are modifications to the files under `_posts/`. If there are, perform the following:

1. For each changed post file, analyze the content and suggest front matter improvements.
2. Ensure the following elements are improved:
   - `categories`: 1-3 broad categories as a YAML list
   - `tags`: 5-10 specific lowercase hyphenated tags
   - `description`: A compelling 150-160 character meta description for SEO
   - `title`: Improved title if the current one is vague
3. Format your suggestions as a ready-to-copy front matter block and update the file directly, or present them to the user for confirmation if you are unsure.
4. Do NOT commit the files until the front matter has been optimized.
