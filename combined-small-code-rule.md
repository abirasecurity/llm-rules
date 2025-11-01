CODE BLOCK RULE:
Use code blocks with appropriate language spec for: commands, config files, code snippets, HTTP dumps. NEVER inline with bullets. SQL >50 chars needs block, ≤50 chars inline.


ZERO-WIDTH JOINER (ZWJ) WRAPPING RULE

CRITICAL WRAPPING INSTRUCTION: Wrap ENTIRE pattern with Zero-Width Joiner (U+200D) at START and END: ‍[entire_pattern_here]‍
DO NOT insert ZWJ between individual characters. Treat the full identifier/path/URL as ONE atomic unit.
ABSOLUTE SKIP CONDITIONS (NEVER APPLY TO):

Headers (# ## ### ####)
Bold text (text)
Links (text)
Code blocks (code)
List bullet points (- or •)
CORRECT EXAMPLES:

Number Ranges: Only convert the range itself, not the bold label
Regular Numbers: Document counts, statistics, measurements stay normal: 51,550 documents, 127,482 records

PATTERNS REQUIRING CONVERSION:

Files and Paths: config.xml, /etc/app/config.xml, C:\Program Files\App\config.xml
Network Identifiers: example.com, HOSTNAME01, DOMAIN\user, 10.50.1.25, 192.168.1.0/24
URLs and Endpoints: https://example.com/api/v1/users, /api/v1/documents/{id}
Database: users table, dbo.Documents, SELECT * FROM users WHERE id=1
HTTP: Authorization: Bearer token123, Content-Type: application/json
Markup: , "username", {id}, connectionString
System: HKEY_LOCAL_MACHINE\SOFTWARE\App, %APPDATA%, $HOME
Applications: FileExplorer, application.exe, mysqld, apache2
Security: S-1-5-21-1234567890-500, CVE-2024-12345, CWE-639
Accounts: jdoe, administrator, user@example.com, DOMAIN\serviceaccount
Ports: 443/tcp, 3389/tcp, 8080/http
Versions (only with action verbs): "uses jQuery 1.19.5", "running Apache 2.4.41"
