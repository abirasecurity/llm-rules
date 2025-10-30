# CODE BLOCK FORMATTING RULE

## MANDATORY IMPLEMENTATION
You MUST apply these code block formatting rules to ALL technical content in vulnerability reports and responses. This rule works in conjunction with existing formatting guidelines and does not override them.

## SCOPE
This rule applies to all commands, configuration content, code snippets, and technical implementation examples that appear in vulnerability reports, remediation steps, and technical documentation.

## REQUIRED CODE BLOCK FORMATTING

### Commands and Executable Content
ALL executable commands must be placed in separate code blocks with appropriate language specification. NEVER place commands inline with bullet points or on the same line as bullets.

**Examples requiring code blocks:**
- Shell commands: `nmap`, `rpcclient`, `curl`, `wget`, `smbclient`
- PowerShell commands: `Get-Command`, `Set-ExecutionPolicy`, `Invoke-WebRequest`
- Database queries: SQL statements **greater than 50 characters** (shorter SQL can remain inline)
- Python/Ruby/Perl scripts or script snippets
- Binary manipulation commands: `strings`, `hexdump`, `objdump`

### Configuration File Content
ALL configuration file content, regardless of length, must be placed in code blocks with language specification matching the file type.

**Examples requiring code blocks:**
- XML configuration: `web.config`, `app.config`, `pom.xml`, `AndroidManifest.xml`
- YAML/YML: `docker-compose.yml`, `.gitlab-ci.yml`, `kubernetes.yaml`
- JSON: `package.json`, `appsettings.json`, `config.json`
- INI/CONF: `.ini` files, Apache `.conf`, nginx configuration
- Registry entries: Windows Registry `.reg` format
- Environment files: `.env`, `.bashrc`, `.profile`
- Apache/IIS configuration: `.htaccess`, `httpd.conf`, IIS `web.config` sections

### Code Snippets and Implementation Examples
ALL code snippets showing implementation examples must be in code blocks, regardless of length.

**Examples requiring code blocks:**
- C#/VB.NET code snippets
- JavaScript/TypeScript code
- PHP, Java, Python, Ruby code examples
- HTML/CSS markup when showing technical implementation
- API request/response bodies
- XML/SOAP payloads
- Regular expressions when shown as implementation code

### HTTP Headers and Requests
HTTP headers presented as technical evidence must be in code blocks when showing:
- Complete HTTP request/response dumps
- Multiple headers together (3+ headers)
- Header values containing technical data (tokens, cookies, CSP policies)

**Single headers with values may remain inline** when used for simple reference: `Content-Type: text/html`

## LANGUAGE SPECIFICATION REQUIREMENTS
Always specify the language for syntax highlighting using the appropriate identifier:

```
bash, shell, sh - Shell commands
powershell, ps1 - PowerShell commands
xml - XML configuration files
yaml, yml - YAML files
json - JSON files
ini - INI files
sql - SQL queries (>50 characters)
python, py - Python code
csharp, cs - C# code
javascript, js - JavaScript code
typescript, ts - TypeScript code
php - PHP code
java - Java code
ruby, rb - Ruby code
html - HTML markup
css - CSS styles
http - HTTP request/response dumps
registry, reg - Windows Registry entries
apache, conf - Apache configuration
nginx - Nginx configuration
```

## SQL QUERY EXCEPTION
SQL queries **50 characters or less** may remain inline using single backticks (e.g., `SELECT * FROM users`). SQL queries **greater than 50 characters** MUST be placed in code blocks with `sql` language specification.

**Inline SQL allowed:**
- `SELECT @@version`
- `EXEC xp_cmdshell 'whoami'`
- `USE database; SELECT TOP 1 * FROM table`

**Code block SQL required:**
```sql
SELECT u.username, u.email, r.role_name 
FROM users u 
INNER JOIN roles r ON u.role_id = r.id 
WHERE u.status = 'active'
```

## FORMATTING EXAMPLES

### Correct Format - Command in Code Block:
**Near Term Actions**

- **Disable SMB Signing:** Configure Group Policy to require SMB signing on all domain controllers. Execute the following PowerShell command on each DC:

```powershell
Set-SmbServerConfiguration -RequireSecuritySignature $true -Force
```

This prevents man-in-the-middle attacks by cryptographically signing all SMB traffic.

### Incorrect Format - Command Inline:
**Near Term Actions**

- **Disable SMB Signing:** Configure Group Policy to require SMB signing by running `Set-SmbServerConfiguration -RequireSecuritySignature $true -Force` on each DC.

### Correct Format - Configuration in Code Block:
**Near Term Actions**

- **Remove Verbose HTTP Headers:** Configure IIS to suppress framework version headers by adding the following to `web.config`:

```xml
<httpProtocol>
  <customHeaders>
    <remove name="X-AspNetMvc-Version" />
    <remove name="X-AspNet-Version" />
  </customHeaders>
</httpProtocol>
```

### Correct Format - Short SQL Inline:
The query `SELECT @@version` returns the SQL Server version without requiring authentication.

### Correct Format - Long SQL in Code Block:
The following query enumerates all database users and their associated permissions:

```sql
SELECT u.name AS UserName, u.type_desc, p.permission_name, p.state_desc
FROM sys.database_principals u
LEFT JOIN sys.database_permissions p ON u.principal_id = p.grantee_principal_id
WHERE u.type IN ('S', 'U', 'G')
ORDER BY u.name
```

## VALIDATION CHECKLIST
Before finalizing any vulnerability report or technical response, verify:

- [ ] All commands are in code blocks with language specification
- [ ] All configuration file content is in code blocks
- [ ] All code snippets are in code blocks
- [ ] SQL queries >50 characters are in code blocks
- [ ] No commands appear on the same line as bullet points
- [ ] Language specifications match content type
- [ ] Code blocks enhance readability and enable copy/paste functionality

## INTEGRATION WITH EXISTING RULES
This rule complements existing formatting guidelines:
- Works with bullet point formatting rules (minimum 2 bullets)
- Works with SQL query length rule (50 character threshold)
- Works with Unicode Mathematical Monospace rules (code blocks are excluded from Unicode conversion)
- Works with inline code formatting rules (single backticks for short technical terms like `filename.txt`, code blocks for executable content)

## EXECUTION PRIORITY
When multiple formatting rules apply:
1. If content is executable or configuration: use code block
2. If SQL query length >50 characters: use code block
3. If simple technical term/identifier: apply Unicode monospace 
4. If filename/path/version: apply Unicode monospace (unless in code block)