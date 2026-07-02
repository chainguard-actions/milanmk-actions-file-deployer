<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.16

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **milanmk--actions-file-deployer/1.16** was hardened automatically. 53 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ }} expressions into shell commands (sub-rule a), allowing script injection. Attacker-controlled inputs and github context values are embedded verbatim into shell strings without being routed through env: variables or properly quoted. Key violations include:
- `${{inputs.sync}}` unquoted in variable assignment: `input_sync=${{inputs.sync}}`
- `${{github.event.inputs.sync}}` unquoted: `input_sync=${{github.event.inputs.sync}}`
- `${{inputs.proxy-forwarding-port}}`, `${{inputs.proxy-port}}`, `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}` interpolated directly into an `ssh` command
- `${{github.event.before}}` unquoted: `git_previous_commit=${{github.event.before}}`
- `${{github.event.pull_request.base.sha}}` unquoted in variable assignment
- `${{inputs.sync-delta-excludes}}` interpolated directly into `git diff` command
- `${{inputs.ftp-mirror-options}}` and `${{inputs.ftp-post-sync-commands}}` interpolated directly into `lftp -c` command strings, allowing arbitrary lftp/shell command injection
- `${{inputs.ssh-options}}` appended unquoted to an ssh command string
- `${{inputs.ftp-options}}` written directly into ~/.lftprc config
- `${{inputs.webhook}}` used as the curl URL argument
- `${{ github.repository }}`, `${{ github.event.head_commit.message }}`, `${{ github.actor }}` and other github context values interpolated into jq arguments and echo statements
- `${{inputs.remote-host}}`, `${{inputs.remote-user}}`, `${{inputs.remote-path}}`, `${{inputs.local-path}}`, `${{inputs.remote-password}}`, `${{inputs.remote-protocol}}`, `${{inputs.ssh-private-key}}`, `${{inputs.proxy-private-key}}` all interpolated directly into shell commands

Locations:

- `action.yml:97`

### unpinned-uses (severity: high)

The 'Upload artifacts' step uses `actions/upload-artifact@v4`, which is pinned to a mutable version tag (`@v4`) rather than an immutable 40-character commit SHA. This exposes the action to supply-chain attacks if the tag is moved to a different commit.

Locations:

- `action.yml:271`

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

Fixed all script injection issues by moving all ${{ }} expressions (inputs.remote-protocol, inputs.remote-host, inputs.remote-user, inputs.remote-password, inputs.ssh-private-key, inputs.proxy, inputs.proxy-host, inputs.proxy-port, inputs.proxy-forwarding-port, inputs.proxy-user, inputs.proxy-private-key, inputs.local-path, inputs.remote-path, inputs.sync, inputs.sync-delta-excludes, inputs.ssh-options, inputs.ftp-options, inputs.ftp-mirror-options, inputs.ftp-post-sync-commands, inputs.webhook, inputs.artifacts, inputs.debug, github.repository, github.workflow, github.job, github.run_id, github.ref, github.event_name, github.actor, github.event.head_commit.message, github.sha, github.event_path, github.event.before, github.event.pull_request.base.sha, github.event.inputs.sync, toJSON(env), toJSON(inputs)) from the run: block into a comprehensive env: block on the Deploy step. The run: block now uses only shell environment variable references. Also pinned actions/upload-artifact@v4 to the full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed four script injection vulnerabilities in action.yml by introducing sanitized local variables at the start of the 'Initialize inputs' section:

1. `input_ssh_options` = INPUT_SSH_OPTIONS with newlines stripped (tr -d '\n\r') — prevents lftp directive injection via ~/.lftprc
2. `input_sync_delta_excludes` = INPUT_SYNC_DELTA_EXCLUDES with newlines stripped, then split into array via `read -ra` — prevents glob expansion and uncontrolled word-splitting in git diff/diff-tree commands
3. `input_ftp_mirror_options` = INPUT_FTP_MIRROR_OPTIONS with newlines and double-quotes stripped (tr -d '\n\r"') — prevents breaking out of the lftp -c double-quoted string
4. `input_ftp_post_sync_commands` = INPUT_FTP_POST_SYNC_COMMANDS with newlines and double-quotes stripped — prevents lftp command injection in both full and delta sync branches

All ${{ inputs.* }} expressions were already correctly placed in the step's env: block; the fix was to sanitize those env vars before use in the shell script.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted variable expansions in the Deploy step of action.yml:
1. Converted apt_quiet string variable to apt_quiet_args array and used "${apt_quiet_args[@]}" for proper quoting without word-splitting issues.
2. Changed all ${proxy_cmd} command-prefix usages to ${proxy_cmd:+"$proxy_cmd"} so the variable is properly quoted when non-empty and absent when empty.
3. Quoted ${git_previous_commit} and ${local_path_unslash} in git cat-file, git diff, and git diff-tree commands.
4. Quoted ${local_path_unslash} and ${remote_path_unslash} inside the lftp -c strings for both full and delta sync modes.
5. Variables on lines 213-217 (${input_ssh_options}, ${INPUT_REMOTE_PROTOCOL}, etc.) are already inside double-quoted echo strings and are protected from shell word splitting.
Note: ${input_ftp_mirror_options} and ${input_ftp_post_sync_commands} inside the lftp -c string are inside a double-quoted shell string, so they're protected from shell word splitting; they're interpreted by lftp, not the shell.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed all script-injection vulnerabilities in action.yml:

1. **Critical sed #e flag**: Replaced two `sed` commands using the `#e` (execute) flag with safe `while IFS= read -r` loops calling `realpath` directly with properly quoted arguments. The `#e` flag caused sed to execute the replacement string as a shell command, and the unquoted user-controlled `$local_path_unslash` enabled arbitrary command injection.

2. **${input_ssh_options} in echo**: Replaced `echo "set sftp:connect-program ... ${input_ssh_options}"` with `printf 'set sftp:connect-program ... %s\n' "${input_ssh_options}"` to prevent command substitution in double-quoted strings.

3. **Enhanced sanitization**: Updated `tr -d` patterns for `input_ssh_options`, `input_ftp_mirror_options`, and `input_ftp_post_sync_commands` to also strip backtick (`` ` ``) and dollar sign (`$`) characters, preventing command substitution when these values are embedded in double-quoted bash strings passed to `lftp -c`.

4. **${local_path_slash} in rsync**: Added double quotes around `"${local_path_slash}"` and `"$HOME/files_to_upload"` in the rsync command to prevent word splitting and glob expansion.

