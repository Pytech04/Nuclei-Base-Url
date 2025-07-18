

#  Usage Guide for `baseurl_paths.txt`

##  File: `baseurl_paths.txt`

This file contains a comprehensive list of base paths intended for use in web reconnaissance, vulnerability scanning, and automated enumeration—particularly in conjunction with tools like [Nuclei](https://github.com/projectdiscovery/nuclei), [ffuf](https://github.com/ffuf/ffuf), [dirsearch](https://github.com/maurosoria/dirsearch), and other similar tools.

---

##  Purpose

The goal of `baseurl_paths.txt` is to provide:

*  A curated list of commonly exposed or misconfigured endpoints
*  Reusable base paths for fuzzing and endpoint discovery
* 🛠 Optimized compatibility with automation tools

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


