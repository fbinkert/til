---
title: 'Remove a file from git'
description: 'How to remove a file from being tracked by Git but keep it on disk'
pubDate: 2025-09-14
author: 'Fabian Binkert'
tags: ['Git']
---
You can remove a file from version control while keeping it on disk. This is
ideal when you accidentally committed something that should be in `.gitignore`.

```shell
git rm --cached <file-path>
```

- `--cached` removes from the index only, the file stays on disk.
