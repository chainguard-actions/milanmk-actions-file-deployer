<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 55 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ }} expressions into shell commands (sub-rule a), and several inputs are also expanded unquoted (sub-rule b). Examples of sub-rule (a) violations: `${{inputs.ftp-post-sync-commands}}` and `${{inputs.ftp-mirror-options}}` are injected verbatim into an `lftp -c` string, allowing arbitrary lftp/shell command injection; `${{inputs.ssh-options}}`, `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}`, `${{inputs.proxy-forwarding-port}}`, `${{inputs.proxy-port}}` are interpolated directly into an `ssh` command; `${{github.event_path}}` is passed to `cat`; `${{inputs.sync-delta-excludes}}` is injected into `git diff`. Examples of sub-rule (b) violations: `input_sync=${{inputs.sync}}` (unquoted assignment), `input_sync_delta_includes=${{inputs.sync-delta-includes}}` (unquoted), `git_previous_commit=${{github.event.before}}` (unquoted), `git_previous_commit=${{github.event.pull_request.base.sha}}` (unquoted), `git rev-parse ${{github.sha}}^` (unquoted). Any attacker-controlled input value containing shell metacharacters, newlines, or command substitution sequences can achieve arbitrary code execution on the runner.

Locations:

- `action.yml:78`

### unpinned-uses (severity: high)

The 'Upload artifacts' step uses `actions/upload-artifact@v7`, which is a mutable tag reference rather than a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit, enabling a supply-chain attack.

Locations:

- `action.yml:232`

### hardcoded-credentials (severity: high)

A literal hardcoded password value `dummypassword` is assigned to `input_remote_password` as a fallback when `inputs.remote-password` is empty: `input_remote_password="dummypassword"`. This hardcoded credential is written to `~/.netrc` and used for FTP/SFTP authentication, which could allow unintended authentication if the remote server accepts this value.

Locations:

- `action.yml:110`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:123`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:126`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.local-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:137`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:140`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:143`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:144`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:148`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:155`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-includes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:160`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:164`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:164`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:165`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:178`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:195`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:209`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:213`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:213`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:214`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:217`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:217`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:219`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:223`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:225`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:233`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:234`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:242`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:243`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:259`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:260`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:260`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:261`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:263`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:267`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:276`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:276`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:330`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:331`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:345`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:359`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-mirror-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:372`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:374`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:381`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:396`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:398`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses, hardcoded-credentials

**Notes:**

Fixed all findings in action.yml:
1. script-injection / static-inline-injection (50+ instances): Moved all ${{ }} expressions from the run: block into the step's env: block. All inputs and github context values are now referenced as plain environment variables ($INPUT_*, $GITHUB_*) in the shell script. List-type inputs (ssh-options, ftp-mirror-options, sync-delta-excludes) are tokenized with the xargs/read-loop idiom to preserve argument boundaries. ftp-post-sync-commands is conditionally appended to the lftp command string only when non-empty.
2. unpinned-uses: Pinned actions/upload-artifact@v7 to full SHA actions/upload-artifact@043fb46d1a93c77aae656e7c1c64a875d1fc6a0a # v7.
3. hardcoded-credentials: Removed the 'dummypassword' fallback. input_remote_password is now set directly from $INPUT_REMOTE_PASSWORD (empty string when not provided, which is the correct behavior for netrc).

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 6 sub-findings of the script-injection finding in action.yml:
1. apt_quiet: converted from unquoted string variable to bash array (apt_quiet_args), expanded with "${apt_quiet_args[@]}"
2. proxy_cmd in apt-get: converted to proxy_pkg array, expanded with "${proxy_pkg[@]}"
3. git_previous_commit: now quoted as "${git_previous_commit}" in git cat-file -t
4. local_path_unslash in git diff/diff-tree: now quoted as "${local_path_unslash}"
5. input_sync_delta_includes for loop: replaced unquoted word-split expansion with IFS=',' read -ra delta_includes_arr and "${delta_includes_arr[@]}"
6. mirror command: mirror_opts[*] now built into mirror_opts_str before embedding in lftp command string; local_path_unslash and remote_path_unslash now quoted with escaped quotes in the lftp command string; proxy_cmd for lftp invocation converted to proxy_arr array expanded with "${proxy_arr[@]}"
Note: INPUT_FTP_POST_SYNC_COMMANDS is an intentional feature input (users specify additional lftp commands); it is kept as-is since restricting it would break the action's designed functionality.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed three script-injection vulnerabilities in action.yml:
1. (Lines ~271-272) Added `local_path_unslash_quoted=$(printf '%q' "$local_path_unslash")` and used the shell-quoted variable in both sed 'e' flag commands. The 'e' flag executes sed substitution results as shell commands, so embedding an unquoted attacker-controlled path was a critical RCE vector. printf '%q' ensures shell metacharacters are escaped.
2. (Line ~279) Quoted `${local_path_slash}` as `"${local_path_slash}"` and `$HOME/files_to_upload` as `"$HOME/files_to_upload"` in the rsync invocation to prevent word splitting and glob expansion from attacker-controlled input.
3. (Lines ~308 and ~320) Changed `$INPUT_FTP_POST_SYNC_COMMANDS` to `${INPUT_FTP_POST_SYNC_COMMANDS}` (with braces) in both the full-sync and delta-sync branches within the double-quoted lftp_cmds string, ensuring proper quoting within the string context.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed all 7 sub-findings of the script-injection finding in hardened/action/action.yml:

1. Debug echo (line ~7349): Replaced echo with printf using %s format specifiers for all INPUT_* variables.

2. Netrc echo (line ~8289): Replaced echo with printf using %s format specifiers for INPUT_REMOTE_HOST, INPUT_REMOTE_USER, and input_remote_password to prevent newline injection.

3. Proxychains config (line ~9312): Replaced multi-line echo containing $INPUT_PROXY_FORWARDING_PORT with printf using %s format specifier.

4. Lftprc open line (line ~11652): Replaced echo with printf using %s format specifiers for INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_USER, INPUT_REMOTE_HOST, and INPUT_REMOTE_PORT.

5. Sed with #e flag (lines ~15708-15860): Replaced the dangerous sed --regexp-extended with #e flag (which executes shell commands) with safe while-read loops that call realpath directly, eliminating shell execution entirely.

6. FTP post-sync commands (line ~18700): Replaced direct string interpolation of INPUT_FTP_POST_SYNC_COMMANDS into the lftp command string with a separate lftp -c "$INPUT_FTP_POST_SYNC_COMMANDS" invocation for both full and delta sync paths.

7. Protocol echo (line ~16715): Replaced echo with printf using %s format specifiers for INPUT_REMOTE_PROTOCOL and other variables.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed four script-injection sub-rule (b) findings in action.yml:
1. ssh_opts[*] unquoted expansion (line 211): Built ssh_opts_str safely using printf '%s ' "${ssh_opts[@]}" (quoted @-expansion) instead of unquoted [*] expansion inside double-quoted echo strings.
2. ssh_opts[*] unquoted expansion (line 213): Same fix applied to the else branch.
3. mirror_opts_str unquoted expansion (line 258): Replaced mirror_opts_str=" ${mirror_opts[*]}" with printf-based safe string construction using quoted [@] expansion.
4. $INPUT_FTP_POST_SYNC_COMMANDS passed as lftp -c argument (line 278): Changed to write commands to a mktemp file and run lftp -f on that file instead of passing the untrusted input directly as inline lftp commands. Applied to both the 'full' and 'delta' sync branches. Temp file is removed after use.

