<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.16

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.16** was hardened automatically. 53 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ }}` expressions into shell commands (sub-rule a), bypassing any shell quoting. This allows an attacker who controls any of these values to inject arbitrary shell commands. Notable high-risk instances include:
- `${{inputs.ftp-post-sync-commands}}` injected verbatim into an `lftp -c "..."` command string (direct command injection)
- `${{inputs.ftp-options}}` injected into the lftp config file content
- `${{inputs.ftp-mirror-options}}` injected into an `lftp -c` command
- `${{inputs.ssh-options}}` appended to lftp config
- `${{inputs.sync-delta-excludes}}` passed unquoted to `git diff`
- `${{inputs.proxy-forwarding-port}}`, `${{inputs.proxy-port}}`, `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}` interpolated directly into an `ssh` command
- `${{inputs.remote-host}}`, `${{inputs.remote-user}}`, `${{inputs.remote-password}}` interpolated into shell strings
- `${{inputs.local-path}}`, `${{inputs.remote-path}}` interpolated into shell commands
- `${{github.event.head_commit.message}}`, `${{github.actor}}`, `${{github.event_name}}`, `${{github.event.before}}`, `${{github.event.pull_request.base.sha}}`, `${{github.sha}}` etc. interpolated throughout
- `${{inputs.webhook}}` used directly in a `curl` command
All of these must be moved to `env:` variables and then double-quoted in the shell script.

Locations:

- `action.yml:68`
- `action.yml:69`
- `action.yml:70`
- `action.yml:71`
- `action.yml:72`
- `action.yml:73`
- `action.yml:74`
- `action.yml:75`
- `action.yml:76`
- `action.yml:79`
- `action.yml:85`
- `action.yml:88`
- `action.yml:91`
- `action.yml:93`
- `action.yml:97`
- `action.yml:99`
- `action.yml:101`
- `action.yml:155`
- `action.yml:163`
- `action.yml:168`
- `action.yml:172`
- `action.yml:176`
- `action.yml:183`
- `action.yml:196`
- `action.yml:197`
- `action.yml:198`
- `action.yml:199`
- `action.yml:219`
- `action.yml:220`
- `action.yml:221`
- `action.yml:222`
- `action.yml:240`
- `action.yml:241`
- `action.yml:242`
- `action.yml:243`
- `action.yml:244`
- `action.yml:260`
- `action.yml:261`
- `action.yml:262`
- `action.yml:263`
- `action.yml:264`
- `action.yml:265`
- `action.yml:279`
- `action.yml:280`
- `action.yml:281`
- `action.yml:282`
- `action.yml:283`
- `action.yml:284`
- `action.yml:285`
- `action.yml:286`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references a mutable version tag (`@v4`) instead of a full 40-character commit SHA. This means the action could be silently replaced with a malicious version via a tag update, enabling a supply-chain attack. It should be pinned to a specific commit SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:302`

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

Rewrote action.yml to fix all security findings:
1. Moved all 38 ${{ }} expressions (inputs.* and github.*) from the run: block to the step's env: block. Each is assigned to a named env var (INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_HOST, GITHUB_SHA_VAL, etc.) and referenced in the shell script with proper double-quoting.
2. List-type inputs (sync-delta-excludes, ftp-mirror-options) are tokenized using the xargs/while-read-d-null pattern to preserve argument boundaries without injection risk.
3. The ftp-options input is written to ~/.lftprc using printf '%s\n' to avoid shell interpretation.
4. The ssh-options input is passed via printf format string to avoid injection into the lftp config.
5. The open line in ~/.lftprc is built using printf with separate format arguments for each field.
6. Pinned actions/upload-artifact@v4 to full SHA: actions/upload-artifact@ea165f8d65b6e75b540449e92b4886f43607fa02 # v4

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all four script-injection findings in hardened/action/action.yml:
1. (line 145) Converted apt_quiet string variable to apt_quiet_args array (--quiet --quiet or empty) and proxy_cmd to proxy_install_args array, both expanded with "${arr[@]}" to avoid word-splitting issues.
2. (lines 218-219) Replaced sed with #e flag (which executes substitution results as shell commands) with a safe while-read loop calling realpath directly on each line from files_to_upload and files_to_delete.
3. (lines 248-271) Replaced lftp -c "...${post_sync_cmd}" with lftp -f script_file approach: lftp commands are written to a mktemp file using printf, and lftp reads the script file directly. This eliminates shell interpolation of user-controlled INPUT_FTP_POST_SYNC_COMMANDS into the shell command string.
4. (line 252) The unquoted ${mirror_opts_args[*]} expansion inside lftp -c is also eliminated by the lftp -f approach: each mirror option is written individually to the script file with printf ' %s' in a for loop.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed the unquoted shell variable expansion in action.yml at the `git cat-file -t` command. Changed `git cat-file -t ${git_previous_commit} &>/dev/null` to `git cat-file -t "${git_previous_commit}" &>/dev/null`. This prevents an attacker from injecting shell metacharacters through the `github.event.before` or `github.event.pull_request.base.sha` context values, which are passed via the `GITHUB_EVENT_BEFORE` and `GITHUB_EVENT_PR_BASE_SHA` environment variables respectively.

