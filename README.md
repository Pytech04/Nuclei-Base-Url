#  Unique Nuclei Template BaseURL Paths 

<img width="2048" height="997" alt="image" src="https://github.com/user-attachments/assets/f9c0655d-8186-46f5-ae5c-d26b25a6f2d8" />








##  What’s Inside
- This repository contains a curated set of unique BaseURL endpoint paths extracted from publicly available YAML files across GitHub.
- A collection of **deduplicated YAML files**, gathered from public GitHub repositories.
- Extracted **endpoint paths** containing `{{BaseURL}}/`, cleaned and filtered.
- **`baseurl_paths.txt`**: A sorted, unique list of paths useful for fuzzing, endpoint discovery, automation, or recon pipelines.

Example entries from `baseurl_paths.txt`:

```
/wp-content/uploads/pdf-invoices/
/xmlrpc/cache/index.html
/xmlrpc/includes/index.html
/Xslt/Web.config
/yarn.lock
```


##  How It Was Built

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



#  Usage Guide for `baseurl_paths.txt`

##  File: `baseurl_paths.txt`

This file contains a comprehensive list of base paths intended for use in web reconnaissance, vulnerability scanning, and automated enumeration—particularly in conjunction with tools like [ffuf](https://github.com/ffuf/ffuf), [dirsearch](https://github.com/maurosoria/dirsearch), and other similar tools.

---

##  Purpose

The goal of `baseurl_paths.txt` is to provide:

*  A curated list of commonly exposed or misconfigured endpoints
*  Reusable base paths for fuzzing and endpoint discovery
*  Optimized compatibility with automation tools

---

##  How to Use

###  With ffuf

```bash
ffuf -u https://example.com/FUZZ -w baseurl_paths.txt
```

###  With dirsearch

```bash
dirsearch -u https://example.com -w baseurl_paths.txt
```

---

##  File Format

* Each line is a separate path or endpoint
* No URL schemes (e.g., `http://`) included—just the base path
* Supports internationalized or Unicode paths (if required)

**Example Entries**:

```
/welcome/views/web2py_ajax.html
/wp-content/plugins/api-bearer-auth/swagger/swagger-config.yaml.php?&server=%3C%2Fscript%3E%3Cscript%3Ealert%28document.domain%29%3C%2Fscript%3E
/wp-content/uploads/pdf-invoices/
/xmlrpc/cache/index.html
/xmlrpc/includes/index.html
/Xslt/Web.config
/yarn.lock
```

---

## Notes

* Cleaned of duplicates and sorted (if you use sorting logic)
* Be mindful of rate limits and scope when using this list against production targets
* Use in accordance with bug bounty or legal pentesting programs

---

##  Contribution

Feel free to contribute by:

* Adding new commonly found paths
* Removing obsolete or deprecated ones
* Optimizing for performance or tool compatibility

Open a PR or submit an issue with suggestions.

---

##  Disclaimer

This file is intended **solely for educational, research, and authorized security testing**. Always obtain proper permission before using it on any system.




