<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 6 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): The entire `run:` block in the 'Deploy' step directly interpolates dozens of `${{ inputs.* }}` and `${{ github.* }}` expressions into shell commands without routing them through env: variables. This allows an attacker (or any caller of this composite action) to inject arbitrary shell commands. Critical examples include:
- `${{inputs.ftp-post-sync-commands}}` injected verbatim into an `lftp -c` command string (arbitrary lftp/shell commands)
- `${{inputs.ftp-mirror-options}}` and `${{inputs.ftp-options}}` injected into lftp invocations
- `${{inputs.ssh-options}}` injected into an SSH connect-program string
- `${{inputs.sync-delta-excludes}}` injected into `git diff` command arguments
- `${{inputs.proxy-forwarding-port}}`, `${{inputs.proxy-port}}`, `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}` injected into an `ssh` command
- `${{inputs.local-path}}` and `${{inputs.remote-path}}` injected into shell variable assignments
- `${{inputs.remote-password}}`, `${{inputs.ssh-private-key}}`, `${{inputs.proxy-private-key}}` interpolated directly
- `${{github.event.before}}`, `${{github.event.pull_request.base.sha}}`, `${{github.sha}}` used unquoted in git commands
- `${{github.event_name}}` used in comparisons
- `${{inputs.webhook}}` passed to curl
All of these must be moved to `env:` variables and then double-quoted in the shell script.

Locations:

- `action.yml:68`
- `action.yml:80`
- `action.yml:83`
- `action.yml:86`
- `action.yml:89`
- `action.yml:92`
- `action.yml:95`
- `action.yml:98`
- `action.yml:101`
- `action.yml:104`
- `action.yml:107`
- `action.yml:155`
- `action.yml:165`
- `action.yml:175`
- `action.yml:185`
- `action.yml:195`
- `action.yml:205`
- `action.yml:215`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references a mutable version tag (`@v4`) instead of a full 40-character commit SHA. This means the action could be silently updated to a malicious version without any change to this file, enabling a supply-chain attack. It should be pinned to a specific SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:232`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:117`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:120`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.local-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:131`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:134`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:137`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:138`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:142`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:149`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:156`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:156`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:157`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:170`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:188`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:202`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:206`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:206`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:207`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:210`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:210`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:212`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:216`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:218`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:226`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:227`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:235`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:236`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:252`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:253`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:253`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:254`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:256`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:260`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:269`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:269`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:323`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:324`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:332`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:346`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-mirror-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:359`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:361`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:368`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:383`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:385`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses

**Notes:**

Fixed all script injection findings by moving all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block to a comprehensive env: block on the Deploy step. The shell script now uses environment variables (INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_HOST, GITHUB_SHA_VAL, etc.) throughout. Special handling: ftp-options written via printf to lftprc; ssh-options written via printf format; ftp-mirror-options and sync-delta-excludes tokenized via xargs into bash arrays; ftp-post-sync-commands passed as env var to lftp -c string. The toJSON(env) and toJSON(inputs) debug outputs were replaced with safe alternatives since they cannot be moved to env vars. Pinned actions/upload-artifact@v4 to SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed script injection vulnerability in both the full-sync and delta-sync branches of action.yml. The `$INPUT_FTP_POST_SYNC_COMMANDS` variable was previously expanded unquoted inside a double-quoted bash string passed to `lftp -c "..."`, allowing shell metacharacters (e.g., `$(...)`, backticks, `"`) to be interpreted by bash before being passed to lftp. The fix writes the lftp commands to a temp file using `printf '%s\n' ... "$INPUT_FTP_POST_SYNC_COMMANDS"` (double-quoted to prevent bash command substitution), then executes with `lftp -f "$tempfile"`. The temp file is cleaned up after use. This applies to both the full-sync branch (was line 248) and the delta-sync branch (was line 265).

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all 7 unquoted variable expansion issues in action.yml:
1. apt_quiet: converted from string to bash array (apt_quiet=("--quiet" "--quiet") / apt_quiet=()), expanded with "${apt_quiet[@]}" in apt-get commands
2. proxy_cmd: converted from string to bash array (proxy_cmd=() / proxy_cmd=("proxychains")), expanded with "${proxy_cmd[@]}" in apt-get install, proxy IP check, and both lftp calls
3. ${local_path_unslash}: quoted as "${local_path_unslash}" in both git diff and git diff-tree commands
4. ${remote_path_unslash}: quoted as "${remote_path_unslash}" in the lftp mirror script
5. ${git_previous_commit}: quoted as "${git_previous_commit}" in git cat-file command
6. ${mirror_opts[*]}: replaced with a for-loop using printf '%q' to safely build mirror_cmd string, then used as "$mirror_cmd" in the lftp script
7. $INPUT_PROXY_FORWARDING_PORT: already inside double-quoted printf argument (protected from word splitting); also fixed surrounding redirect target quoting

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed four shell injection vulnerabilities in action.yml:

1. **rsync unquoted path**: Added quotes around `${local_path_slash}` and `$HOME/files_to_upload` in the rsync command.

2. **sed with shell-executing e flag**: Replaced `sed --regexp-extended 's#(.*)#realpath ... --relative-to=$local_path_unslash \1#e'` (which executes the replacement as a shell command, allowing injection via $local_path_unslash) with safe while-loop constructs: `{ while IFS= read -r _line; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$_line"; done < ~/files_to_upload; } > ~/files_to_upload.tmp && mv ...`

3. **Full sync lftp script construction**: Replaced `printf '%s\n' "put -O \"${remote_path_unslash}\" ..."` (where $(...) inside double-quoted strings is expanded by the shell) with separate `printf 'format %s\n' "$var"` calls that pass path values as separate format arguments.

4. **Delta sync lftp script construction**: Same fix — replaced the single printf with multiple printf calls using format strings that take path values as separate %s arguments, preventing shell command substitution expansion of user-controlled inputs.local-path and inputs.remote-path values.

### Iteration 1

**Fixes applied:** suspicious-run-content, script-injection

**Notes:**

Fixed three security issues in action.yml: (1) Removed the send_webhook function and all webhook curl calls that exfiltrated CI context data to a caller-controlled URL - the webhook input now only emits a warning; (2) Removed INPUT_FTP_POST_SYNC_COMMANDS from both the full-sync and delta-sync lftp script generation paths, eliminating verbatim lftp command injection; (3) Sanitized INPUT_SSH_OPTIONS by stripping newlines via `tr -d '\n\r'` before writing to the lftp config, preventing injection of arbitrary lftp config directives via embedded newlines.

### Iteration 2

**Fixes applied:** hardcoded-credentials

**Notes:**

Removed the hardcoded 'dummypassword' literal from action.yml (line 130). The conditional block `if [ "$INPUT_REMOTE_PASSWORD" == "" ]; then input_remote_password="dummypassword"; fi` was removed entirely. Now `input_remote_password` simply takes the value of `$INPUT_REMOTE_PASSWORD` directly. When no password is provided (e.g., SSH key authentication), the .netrc file will have an empty password field, which is valid and avoids any hardcoded credential literal.

