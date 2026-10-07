<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 54 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' step's run: block directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions into shell commands (sub-rule a). This allows an attacker to inject arbitrary shell commands. Particularly dangerous examples include:
- `${{ github.event.head_commit.message }}` (attacker-controlled via commit message) passed as a jq --arg value (line ~116)
- `${{ github.event.inputs.sync }}` (workflow_dispatch input) assigned unquoted: `input_sync=${{github.event.inputs.sync}}` (line ~138)
- `${{ github.event.before }}` and `${{ github.event.pull_request.base.sha }}` assigned unquoted to shell variables (lines ~152–156)
- `${{ inputs.ftp-options }}` written directly into ~/.lftprc config file (line ~189)
- `${{ inputs.ssh-options }}` appended unquoted to an echo command (lines ~196–198)
- `${{ inputs.ftp-mirror-options }}` and `${{ inputs.ftp-post-sync-commands }}` interpolated directly into lftp -c shell strings (lines ~222–229)
- `${{ inputs.remote-password }}`, `${{ inputs.ssh-private-key }}`, `${{ inputs.proxy-private-key }}` interpolated directly (lines ~130–133, ~168, ~173)
- `${{ inputs.sync-delta-excludes }}` appended directly to git diff commands (lines ~213–214)
None of these are routed through env: variables; all are raw template substitutions into the shell script before the shell ever sees them.

Locations:

- `action.yml:98`

### unpinned-uses (severity: high)

The 'Upload artifacts' step uses `actions/upload-artifact@v7`, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently replaced by a malicious version without any change to this file. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v7`.

Locations:

- `action.yml:244`

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

1. Moved all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block into an env: block on the Deploy step. Created named environment variables for all 24 inputs and 13 github context values. The shell script now references them as $INPUT_REMOTE_PROTOCOL, $INPUT_WEBHOOK, $GITHUB_SHA_VAL, etc. This fixes all 50+ script-injection and static-inline-injection findings.
2. Pinned actions/upload-artifact@v7 to its full commit SHA: actions/upload-artifact@cf430e030ddbb5b0abf93d22962f4752f3646cd9 # v7.
3. List-style inputs (sync-delta-excludes, ftp-mirror-options) are now tokenized using the xargs/while-read-loop pattern to preserve argument boundaries.
4. The ftp-options input is written to ~/.lftprc using printf '%s' to avoid treating leading dashes as printf flags.
5. The debug section no longer uses ${{ toJSON(inputs) }} or ${{ toJSON(env) }} (which are not injectable but were replaced with equivalent env var references for consistency).

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script-injection vulnerabilities in action.yml:

1. Lines 218/220 (INPUT_SSH_OPTIONS): Sanitized with `tr -d '\n\r'` before writing to ~/.lftprc; used `printf '%s\n'` instead of `echo`.

2. Line 222 (INPUT_REMOTE_PROTOCOL/USER/HOST/PORT): Sanitized all four variables with `tr -d '\n\r'` before writing the `open` directive to ~/.lftprc.

3. Line 285 (input_sync_delta_includes): Replaced unquoted `for i in ${var//,/ }` (glob-expansion risk) with xargs-based tokenization into a bash array, then properly quoted array iteration.

4. Lines 290/291 (sed with 'e' flag - critical RCE): Replaced `sed --regexp-extended 's#(.*)#realpath ... $local_path_unslash \1#e'` with a safe `while IFS= read -r line; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$line"; done` loop using a mktemp file for atomic replacement.

5. Lines 320/330 (${ftp_post_sync} in lftp -c): Replaced unquoted interpolation of user-controlled post-sync commands inside `lftp -c "..."` strings with a temp-file approach: write all lftp commands (including post-sync) to a mktemp file using `printf '%s\n'`, then execute with `lftp -f scriptfile`.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed two script injection vulnerabilities in hardened/action/action.yml:
1. Line ~374: Quoted `${git_previous_commit}` in `git cat-file -t "${git_previous_commit}"` to prevent word splitting/glob expansion on attacker-controllable GitHub context values.
2. Line ~406: Quoted `${local_path_slash}` in the rsync command to `"${local_path_slash}"` to prevent word splitting/glob expansion on user-controlled input from `inputs.local-path`.

### Iteration 4

**Fixes applied:** hardcoded-credentials, script-injection

**Notes:**

1. hardcoded-credentials (line 113): Replaced the literal placeholder 'dummypassword' with '$(openssl rand -hex 16)' to generate a random value at runtime instead of embedding a hardcoded credential. 2. script-injection (line 295): Replaced the unquoted array expansion '${ftp_mirror_opts[*]+${ftp_mirror_opts[*]}}' in the printf argument with a properly quoted per-element loop: 'for _opt in "${ftp_mirror_opts[@]}"; do printf ' "%s"' "$_opt"; done'. Each lftp mirror option is now individually double-quoted when written to the lftp script file, preventing shell metacharacters from escaping the argument context.

### Iteration 5

**Fixes applied:** script-injection

**Notes:**

Fixed two script-injection findings in action.yml:
1. Line ~163: Quoted `${proxy_cmd}` as `"${proxy_cmd}"` in the `sudo apt-get ... install lftp` command to prevent word-splitting and glob expansion.
2. Lines ~196/198: Restructured the two `printf` commands that write to `~/.lftprc` to use `printf 'set sftp:connect-program ... %s\n' "${safe_ssh_options}"` instead of embedding the variable inside a double-quoted string. This ensures `${safe_ssh_options}` is passed as a properly double-quoted argument to printf via `%s`, preventing shell metacharacters (`;`, `|`, `$()`, backticks) in the value from being interpreted by the shell.

