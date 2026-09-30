<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.17

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.17** was hardened automatically. 54 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The composite action's single `run:` block directly interpolates dozens of `${{ }}` expressions into shell commands (rule a), allowing an attacker to inject arbitrary shell commands. Affected expressions include attacker-controllable inputs and github context values:

• `${{inputs.webhook}}` — used as a curl URL and in a conditional (lines ~76, ~79)
• `${{inputs.local-path}}` — passed to `echo … | sed` (line ~88)
• `${{inputs.remote-path}}` — passed unquoted to `realpath` (line ~90)
• `${{inputs.remote-password}}` — interpolated directly into shell variable assignment (line ~93)
• `${{inputs.proxy}}` — interpolated directly (line ~97)
• `${{inputs.sync}}` — assigned unquoted: `input_sync=${{inputs.sync}}` (line ~103)
• `${{inputs.sync-delta-includes}}` — assigned unquoted: `input_sync_delta_includes=${{inputs.sync-delta-includes}}` (line ~107)
• `${{inputs.remote-protocol}}` — used in conditionals and echo (lines ~110, ~148, ~155)
• `${{inputs.debug}}` — used in conditionals throughout (lines ~116, ~127, ~133, etc.)
• `${{github.event_name}}` — used in conditionals (lines ~104, ~106, ~200, ~207, ~211)
• `${{github.event.inputs.sync}}` — interpolated directly (line ~105)
• `${{github.event_path}}` — passed to `cat` (line ~128)
• `${{inputs.remote-host}}`, `${{inputs.remote-user}}` — written into ~/.netrc and ~/.lftprc (lines ~149, ~172)
• `${{inputs.ssh-private-key}}`, `${{inputs.proxy-private-key}}` — written to key files (lines ~155, ~162)
• `${{inputs.proxy-forwarding-port}}` — passed directly to `ssh -D` and `socks5` config (lines ~166, ~220)
• `${{inputs.ftp-options}}` — interpolated into ~/.lftprc content (line ~183)
• `${{inputs.ssh-options}}` — appended to sftp:connect-program line (lines ~186, ~188)
• `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}`, `${{inputs.proxy-port}}` — passed directly to `ssh` command (line ~220)
• `${{github.event.before}}`, `${{github.event.pull_request.base.sha}}` — assigned unquoted to shell variable (lines ~207, ~209)
• `${{github.sha}}` — used in git commands and echo (lines ~212, ~228, ~237)
• `${{inputs.sync-delta-excludes}}` — passed directly to `git diff` (lines ~241, ~242)
• `${{inputs.ftp-mirror-options}}` — interpolated into lftp -c command string (line ~285)
• `${{inputs.ftp-post-sync-commands}}` — interpolated into lftp -c command string (lines ~287, ~296)
• `${{inputs.artifacts}}` — used in conditionals (lines ~252, ~307)
• `${{github.event.head_commit.message}}` — interpolated into echo (lines ~72, ~228)
• `${{github.actor}}`, `${{github.repository}}`, `${{github.ref}}`, `${{github.workflow}}`, `${{github.job}}`, `${{github.run_id}}` — interpolated into jq args and echo (lines ~65–75, ~228)

All of these allow shell metacharacter injection since the values are substituted by the Actions runner before the shell ever sees the script.

Locations:

- `action.yml:65`
- `action.yml:76`
- `action.yml:79`
- `action.yml:88`
- `action.yml:90`
- `action.yml:93`
- `action.yml:97`
- `action.yml:103`
- `action.yml:105`
- `action.yml:107`
- `action.yml:110`
- `action.yml:128`
- `action.yml:148`
- `action.yml:155`
- `action.yml:162`
- `action.yml:166`
- `action.yml:183`
- `action.yml:186`
- `action.yml:220`
- `action.yml:228`
- `action.yml:241`
- `action.yml:285`
- `action.yml:287`
- `action.yml:296`

### unpinned-uses (severity: high)

The `Upload artifacts` step uses `actions/upload-artifact@v4`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling a supply-chain attack. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:316`

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

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses

**Notes:**

1. Moved all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block to the step's env: block in the Deploy step. All 39 expressions (inputs.webhook, inputs.local-path, inputs.remote-path, inputs.remote-password, inputs.proxy, inputs.sync, inputs.sync-delta-includes, inputs.sync-delta-excludes, inputs.remote-protocol, inputs.remote-host, inputs.remote-user, inputs.remote-port, inputs.ssh-private-key, inputs.proxy-private-key, inputs.proxy-forwarding-port, inputs.proxy-user, inputs.proxy-host, inputs.proxy-port, inputs.ssh-options, inputs.ftp-options, inputs.ftp-mirror-options, inputs.ftp-post-sync-commands, inputs.artifacts, inputs.debug, github.repository, github.workflow, github.job, github.run_id, github.ref, github.event_name, github.actor, github.event.head_commit.message, github.sha, github.event_path, github.event.before, github.event.pull_request.base.sha, github.event.inputs.sync, toJSON(env), toJSON(inputs)) are now in the env: block. The run: block references only plain $VAR_NAME environment variables.
2. Pinned actions/upload-artifact@v4 to immutable SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with # v4 comment.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed 5 unquoted variable expansions in the Deploy step's run script:
1. $INPUT_FTP_OPTIONS: Changed from unquoted at end of echo string to its own double-quoted argument: '"$INPUT_FTP_OPTIONS"'
2. $INPUT_SSH_OPTIONS (2 occurrences): Changed from unquoted inside echo strings to properly double-quoted using adjacent string concatenation: '""$INPUT_SSH_OPTIONS"'
3. $INPUT_SYNC_DELTA_EXCLUDES (2 occurrences): Changed from unquoted trailing argument in git diff/diff-tree commands to '"$INPUT_SYNC_DELTA_EXCLUDES"'
4. $INPUT_FTP_MIRROR_OPTIONS: Changed from unquoted inside lftp -c string to properly double-quoted using adjacent string concatenation: '""$INPUT_FTP_MIRROR_OPTIONS""'
5. $INPUT_FTP_POST_SYNC_COMMANDS (2 occurrences): Changed from unquoted at end of lftp -c strings to properly double-quoted using adjacent string concatenation: '""$INPUT_FTP_POST_SYNC_COMMANDS"'

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed four script-injection vulnerabilities in action.yml:

1. **$INPUT_PROXY_FORWARDING_PORT** (line ~183): Replaced multiline double-quoted echo with `printf '%s\n'` calls where each argument is individually quoted, preventing newline injection into the proxychains config.

2. **$INPUT_FTP_OPTIONS** (line ~196): The echo string used `"$INPUT_FTP_OPTIONS"` where the leading `"` closed the outer double-quoted string, leaving the variable unquoted. Rewrote the entire lftprc creation block using `{ printf ...; } > ~/.lftprc` with all variables properly quoted.

3. **$INPUT_SSH_OPTIONS** (lines ~211, 213): The pattern `""$INPUT_SSH_OPTIONS"` closed the outer double-quoted string. Replaced with `printf '%s %s\n' "set sftp:connect-program ..." "$INPUT_SSH_OPTIONS"` to keep the variable properly quoted.

4. **$INPUT_FTP_MIRROR_OPTIONS** and **$INPUT_FTP_POST_SYNC_COMMANDS** (lines ~310, 313, 322): The `""$VAR""` patterns closed the outer double-quoted string in `lftp -c` commands. Replaced with a temp-file approach: write lftp commands to a mktemp file using `printf '%s\n'` with properly quoted variables, then execute with `lftp -f "$lftp_script"` instead of `lftp -c`.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed all script-injection vulnerabilities in action.yml:
1. Quoted `$git_previous_commit` and `$local_path_unslash` in git diff/diff-tree commands to prevent word splitting and glob expansion.
2. Replaced the critically dangerous `sed --regexp-extended 's#(.*)#realpath ... $local_path_unslash \1#e'` (which executes the replacement as a shell command via the #e flag) with a safe `while IFS= read -r filepath; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$filepath"; done` loop for both files_to_upload and files_to_delete.
3. Replaced the unquoted `for i in ${input_sync_delta_includes//,/ }` loop with a safe `while IFS= read -r sync_include_item` loop using process substitution with `tr ',' '\n'` to split on commas without word splitting or glob expansion.
4. Fixed unquoted `${proxy_cmd}` in apt-get install by using a bash array `apt_pkgs` that conditionally includes the proxy package.
5. Fixed unquoted `${proxy_cmd}` in the proxy IP check command by using a bash array `proxy_run`.
6. Fixed unquoted `${proxy_cmd}` in both lftp invocations (full sync and delta sync) by using a bash array `lftp_cmd` that conditionally prepends the proxy command.

### Iteration 5

**Fixes applied:** script-injection, hardcoded-credentials

**Notes:**

Fixed two issues in hardened/action/action.yml: (1) script-injection: Quoted the unquoted ${local_path_slash} variable in the rsync command (line ~253) as "${local_path_slash}" to prevent word-splitting and glob expansion on the attacker-controllable inputs.local-path value. (2) hardcoded-credentials: Removed the hardcoded 'dummypassword' fallback (lines ~162-164) — the input_remote_password variable now simply holds $INPUT_REMOTE_PASSWORD directly, using an empty string when no password is provided, eliminating the risk of unintended FTP authentication with a hardcoded credential.

