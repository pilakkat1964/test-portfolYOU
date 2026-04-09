# Local Build and Test – Jekyll Portfolio (`portfolYOU`)

## 1. Ruby Version Requirement

**Question:**  
> What version of Ruby is needed for Jekyll theme `portfolYOU`?  

**Answer:**
- Jekyll 3.8.x works best with **Ruby 2.5 – 2.7**.  
- For `portfolYOU` theme (tested on Jekyll 3.8.7), Ruby **2.7.8** was used.  

**Installed Version Check:**
```bash
ruby -v
# ruby 2.7.8p220
```

---

## 2. Initial `jekyll doctor` Errors

**Command:**
```bash
bundle exec jekyll doctor
```

**Output:**
```text
Configuration file: /home/sysadmin/workspace/GitHub/test/portfolYOU/_config.yml
To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
Remote Theme: Using theme yousinix/portfolyou
Warning: You didn't set an URL in the config file, you may encounter problems with some plugins.
jekyll 3.8.7 | Error:  undefined method `absolute?' for nil:NilClass
```

**Problem:**
- `_config.yml` missing `url` key → caused `url_absolute?` to fail.  

---

## 3. Step 1: Adding `url` Key

**Fix:**
Add the following to `_config.yml`:  
```yaml
url: "http://localhost:4000"  # Temporary for local testing
```

**Rerun Doctor:**
```bash
bundle exec jekyll doctor
```

**Result:**
- `undefined method 'absolute?'` error disappeared  
- Warning about missing URL resolved  

---

## 4. Step 2: Address Minor Warnings

- **Faraday Retry Warning:**
```text
To use retry middleware with Faraday v2.0+, install `faraday-retry` gem
```
- Optional for local build; no impact on Jekyll execution.  

- **Remote Theme Warning:**
```text
Remote Theme: Using theme yousinix/portfolyou
```
- Informational; ensures theme fetched from GitHub.  

---

## 5. Step 3: Local Build

**Build Command:**
```bash
bundle exec jekyll build
```

**Output:**
```text
Configuration file: /home/sysadmin/workspace/GitHub/test/portfolYOU/_config.yml
...
Build completed successfully in XX seconds
```

---

## 6. Step 4: Local Serve

**Command:**
```bash
bundle exec jekyll serve
```

**Result:**
- Local site accessible at `http://localhost:4000`  
- Theme rendered correctly  
- No errors or warnings blocking execution  

---

## 7. Summary of Errors and Fixes

| Error / Warning | Cause | Resolution |
|-----------------|-------|------------|
| `undefined method 'absolute?' for nil:NilClass` | Missing `url` in `_config.yml` | Add `url: "http://localhost:4000"` |
| Faraday retry warning | Faraday v2+ without retry middleware | Optional: install `faraday-retry` gem |
| Remote theme warning | Using remote theme without URL | Ensure `url` is set |
| Build / serve path confusion | `Gemfile` and `_config.yml` locations | `Gemfile` at root, `_config.yml` at root (or `/docs` if using docs folder) |

---

## 8. Lessons Learned

1. **Ruby version matters:** Jekyll 3.8.x works best on Ruby 2.5–2.7.  
2. **URL is mandatory:** Always define `url` in `_config.yml` to avoid `absolute?` errors.  
3. **Remote themes need a URL** even for local builds.  
4. **Run commands from root** where `Gemfile` exists.  
5. Minor warnings (Faraday, remote theme) may not block local builds but should be noted.

