# 🧾 Unique YAML BaseURL Paths Extractor

This repository contains a curated set of unique BaseURL endpoint paths extracted from publicly available YAML files across GitHub.

## 📦 What’s Inside

- A collection of **deduplicated YAML files**, gathered from public GitHub repositories.
- Extracted **endpoint paths** containing `{{BaseURL}}/`, cleaned and filtered.
- **`baseurl_paths.txt`**: A sorted, unique list of paths useful for fuzzing, endpoint discovery, automation, or recon pipelines.

Example entries from `baseurl_paths.txt`:

/wp-content/uploads/pdf-invoices/
/xmlrpc/cache/index.html
/xmlrpc/includes/index.html
/Xslt/Web.config
/yarn.lock


## ⚙️ How It Was Built

> _Skip this if you're only interested in the final data. This section is for transparency and reproducibility._

1. Searched GitHub for `.yaml` files using dorks.
2. Downloaded the identified YAMLs into a single folder.
3. Used `sha256sum` to remove duplicate files by hash.
4. Extracted lines containing `{{BaseURL}}/` using `grep`, `awk`, and `tr`.
5. Sorted and deduplicated the output with `sort -u`.

```bash
grep -rl 'yaml' . | while read -r file; do
  grep '{{BaseURL}}/' "$file" | awk -F '{{BaseURL}}' '{print $2}' | tr -d '"'\'''
done | sort -u > baseurl_paths.txt
```

