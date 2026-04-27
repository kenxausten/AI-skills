---
inclusion: manual
---

# AI-Generated Code Annotation Rules

All AI-generated code MUST be wrapped with `@AI_GENERATED` start and end markers using the file's native comment syntax. This enables traceability, auditing, and tracking.

## Tag Format

- Start marker: `@AI_GENERATED` (optionally followed by `: <description>`)
- End marker: `@AI_GENERATED: end`
- Both markers go on their own lines, immediately before and after the generated block.
- Do NOT nest markers. Each generated block gets its own pair.
- When modifying an existing annotated block, preserve the markers.

## Comment Syntax Reference

| File Type | Start | End |
|---|---|---|
| Go, JS, TS, Java, C, C++, Rust, Proto | `// @AI_GENERATED` | `// @AI_GENERATED: end` |
| Python, Shell, YAML, Makefile | `# @AI_GENERATED` | `# @AI_GENERATED: end` |
| SQL, Lua | `-- @AI_GENERATED` | `-- @AI_GENERATED: end` |
| HTML, XML, Markdown | `<!-- @AI_GENERATED -->` | `<!-- @AI_GENERATED: end -->` |
| CSS, SCSS | `/* @AI_GENERATED */` | `/* @AI_GENERATED: end */` |
| INI, TOML, .env, .properties, .conf | `# @AI_GENERATED` | `# @AI_GENERATED: end` |
| Plain text (.txt) | `# @AI_GENERATED` | `# @AI_GENERATED: end` |
| Dockerfile | `# @AI_GENERATED` | `# @AI_GENERATED: end` |
| HCL (Terraform), Nginx conf | `# @AI_GENERATED` | `# @AI_GENERATED: end` |
| Ruby, Perl, R, Elixir, PowerShell, GraphQL | `# @AI_GENERATED` | `# @AI_GENERATED: end` |
| .gitignore, .dockerignore, .editorconfig | `# @AI_GENERATED` | `# @AI_GENERATED: end` |
| Kotlin, Swift, Scala, Dart, Groovy | `// @AI_GENERATED` | `// @AI_GENERATED: end` |
| Batch (.bat, .cmd) | `REM @AI_GENERATED` | `REM @AI_GENERATED: end` |
| Vue, Svelte (template section) | `<!-- @AI_GENERATED -->` | `<!-- @AI_GENERATED: end -->` |
| Vue, Svelte (script/style section) | Use the syntax of the embedded language (`//` or `/* */`) | |

JSON has no native comments. Use `"_comment": "@AI_GENERATED"` and `"_comment_end": "@AI_GENERATED: end"` fields when needed.

**Fallback rule:** If a file type is not listed above, use the file's native single-line or block comment syntax. If the file has no comment syntax at all, skip annotation.

For files with no standard comment syntax and where adding markers would break functionality (e.g., strict CSV parsers, .log files, binary files), skip annotation entirely.

## Files to NEVER Annotate

The following file types must NOT be annotated as markers would break parsing, builds, or runtime:

- `.csv` — no comment syntax; markers become data rows and corrupt parsing
- `.log` — typically program output, not authored; markers interfere with log parsers
- `.lock` files (package-lock.json, yarn.lock, Gemfile.lock, etc.) — auto-generated, never manually edit
- Binary files (images, compiled assets, archives)
- JSON files with `additionalProperties: false` in their schema (markers cause validation errors)
- XML files with strict DTD/XSD validation where comments in certain positions cause failures

## Special Considerations

- YAML: Place `# @AI_GENERATED` after the `---` document separator, not before it. Some parsers reject content before `---`.
- INI: Most parsers support `#` comments, but some Windows-style parsers only recognize `;`. If targeting Windows-only INI parsers, use `; @AI_GENERATED` and `; @AI_GENERATED: end` instead.
- Proto (protobuf): Use `//` style comments. Do NOT place markers inside `message` or `enum` definitions where they could interfere with code generation tools.
- Makefile: Ensure markers are NOT placed on recipe lines (indented with tab). Place them before the target declaration.

## Placement Rules

- Entire AI-generated file: markers at the very top and bottom of the file.
- Function/class/type level: markers immediately before and after the declaration.
- Inline block within a manual function: markers around only the generated lines.

## Examples

Go / JS / TS / Java:
```go
// @AI_GENERATED
func ValidateUser(user *User) error {
    if user.Email == "" {
        return errors.New("email required")
    }
    return nil
}
// @AI_GENERATED: end
```

Python / Shell / YAML:
```python
# @AI_GENERATED
def process(items: list) -> dict:
    valid = [i for i in items if i.get('is_valid')]
    return {'avg': sum(i['value'] for i in valid) / len(valid)}
# @AI_GENERATED: end
```

SQL:
```sql
-- @AI_GENERATED
SELECT DATE(event_time) AS day, COUNT(DISTINCT user_id) AS active_users
FROM user_events
WHERE event_time > CURRENT_DATE - INTERVAL '7 days'
GROUP BY 1;
-- @AI_GENERATED: end
```

HTML / Markdown:
```html
<!-- @AI_GENERATED -->
<div class="container">
  <h1>Generated Content</h1>
</div>
<!-- @AI_GENERATED: end -->
```

Inline block within manual code:
```go
func ProcessData(data []byte) error {
    // manual code...

    // @AI_GENERATED
    transformed := transform(data)
    validated := validate(transformed)
    // @AI_GENERATED: end

    // more manual code...
}
```

JSON (common config):
```json
{
  "_comment": "@AI_GENERATED",
  "name": "my-app",
  "version": "1.0.0",
  "scripts": {
    "build": "tsc && node dist/index.js",
    "test": "vitest --run"
  },
  "_comment_end": "@AI_GENERATED: end"
}
```

INI / .properties:
```ini
# @AI_GENERATED
[database]
host = localhost
port = 5432
name = app_db
# @AI_GENERATED: end
```

TOML:
```toml
# @AI_GENERATED
[server]
host = "0.0.0.0"
port = 8080
workers = 4
# @AI_GENERATED: end
```

.env:
```env
# @AI_GENERATED
DATABASE_URL=postgres://localhost:5432/app_db
REDIS_URL=redis://localhost:6379
LOG_LEVEL=info
# @AI_GENERATED: end
```

Dockerfile:
```dockerfile
# @AI_GENERATED
FROM node:20-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build
# @AI_GENERATED: end
```

HCL (Terraform):
```hcl
# @AI_GENERATED
resource "aws_s3_bucket" "data" {
  bucket = "my-data-bucket"
  tags = {
    Environment = "production"
  }
}
# @AI_GENERATED: end
```

Plain text (.txt):
```text
# @AI_GENERATED
This content was generated by AI.
Please review before use.
# @AI_GENERATED: end
```

YAML (note: place marker after `---`):
```yaml
---
# @AI_GENERATED
server:
  host: 0.0.0.0
  port: 8080
# @AI_GENERATED: end
```

## Markdown and JSON Annotation Policy

For Markdown and JSON files, apply annotations when they do not break parsing or functionality:

### Markdown Files
- Use `<!-- @AI_GENERATED -->` and `<!-- @AI_GENERATED: end -->` as normal.
- HTML comments are invisible when rendered and do not affect Markdown parsers, so always annotate AI-generated Markdown files (including Kiro spec files like requirements.md, design.md, tasks.md).

### JSON Files
- Use `"_comment": "@AI_GENERATED"` and `"_comment_end": "@AI_GENERATED: end"` by default.
- For OpenAPI/Swagger JSON files, use spec-compliant extension fields instead: `"x-ai-generated": true` at the top-level object.
- For JSON files consumed by strict schema validators with `additionalProperties: false`, do NOT add annotation fields and skip annotation entirely.
- For common config JSON files (package.json, tsconfig.json, etc.), annotation fields are safe since these tools ignore unknown fields.

## When to Tag

- Tag all AI-generated code: functions, types, config blocks, scripts, migrations.
- Tag AI-generated Markdown and JSON files following the policy above.
- Tag ALL AI-generated or AI-modified code, including single-line changes. No exceptions.
- Do NOT tag code that has been significantly rewritten by a human.
- If you make minor edits to an annotated block, keep the markers.
- If you substantially rewrite an annotated block, remove the markers.

## Review Expectations

- All AI-generated code must be reviewed before committing.
- Verify correctness, test coverage, security, and compliance with project standards.
- Never skip testing for generated code.
