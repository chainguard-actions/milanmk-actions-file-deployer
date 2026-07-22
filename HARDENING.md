<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.15** was hardened automatically. 53 finding(s) were identified and resolved across 6 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions into shell commands (sub-rule a). Before the shell ever sees the script, GitHub Actions substitutes these template values verbatim into the shell string, allowing an attacker-controlled calling workflow to inject arbitrary shell commands. Representative offending lines include:
- `--arg repository "${{ github.repository }}"` (and actor, workflow, job, ref, event_name, head_commit.message, sha) inside a jq call
- `curl ... "${{inputs.webhook}}"` — webhook URL injected directly
- `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)` — local-path injected into command substitution
- `remote_path_unslash=$(realpath --canonicalize-missing '${{inputs.remote-path}}')` — remote-path injected
- `input_remote_password="${{inputs.remote-password}}"` — password injected
- `input_sync=${{inputs.sync}}` — unquoted, no braces around expression
- `if [ "${{inputs.remote-protocol}}" != "sftp" ]` — protocol injected into condition
- `${{inputs.ftp-options}}" > ~/.lftprc` — arbitrary lftp options written to config file
- `echo "set sftp:connect-program /usr/bin/ssh -a -x ... ${{inputs.ssh-options}}" >> ~/.lftprc` — ssh options injected
- `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — proxy params injected into ssh command
- `git diff ... ${{inputs.sync-delta-excludes}}` — excludes injected into git command
- `mirror ... ${{inputs.ftp-mirror-options}} ...` — mirror options injected into lftp
- `${{inputs.ftp-post-sync-commands}}` — arbitrary lftp commands injected
All of these must be routed through env: variables and then double-quoted in the shell script.

Locations:

- `action.yml:76`

### unpinned-uses (severity: high)

The 'Upload artifacts' step uses `actions/upload-artifact@v4`, which is a mutable tag reference. If the tag is moved or the repository is compromised, a different (potentially malicious) version of the action could be executed. This should be pinned to a full 40-character commit SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:248`

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

1. Moved all ${{ inputs.* }} and ${{ github.* }} expressions from the run: shell block into a comprehensive env: block on the Deploy step. Created named environment variables for all 23 inputs and 13 github context values. The shell script now references these safely via $VAR_NAME syntax, preventing shell injection attacks.
2. Pinned actions/upload-artifact@v4 to its full commit SHA: actions/upload-artifact@ea165f8d65b6e75b540449e92b4886f43607fa02 # v4.
3. The lftprc configuration block was refactored from a heredoc-style string interpolation to a bash { echo ...; } > file pattern to safely write the ftp-options input via printf '%s\n' "$INPUT_FTP_OPTIONS".
4. The debug section that previously used ${{toJSON(env)}} and ${{toJSON(inputs)}} was simplified to avoid those expressions since they cannot be safely moved to env: (they are template functions, not simple values).

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed four instances of unquoted shell variables sourced from workflow inputs in action.yml:
1. $INPUT_SSH_OPTIONS (lines 218, 220): Replaced echo with printf '%s %s\n' to properly double-quote the variable when writing to ~/.lftprc
2. $INPUT_SYNC_DELTA_EXCLUDES (lines 258, 259): Added double-quotes around the variable in both git diff and git diff-tree commands
3. $INPUT_FTP_MIRROR_OPTIONS (line 299): Changed to ${INPUT_FTP_MIRROR_OPTIONS} with explicit braces inside the lftp -c double-quoted string
4. $INPUT_FTP_POST_SYNC_COMMANDS (lines 301, 309, 311): Changed to ${INPUT_FTP_POST_SYNC_COMMANDS} with explicit braces in both full and delta sync lftp -c command strings

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted expansion of user-controlled input variables in lftp command strings. Added two local variable assignments with proper double-quoting: `ftp_mirror_options="${INPUT_FTP_MIRROR_OPTIONS}"` and `ftp_post_sync_commands="${INPUT_FTP_POST_SYNC_COMMANDS}"`. Replaced all four unquoted occurrences of `${INPUT_FTP_MIRROR_OPTIONS}` and `${INPUT_FTP_POST_SYNC_COMMANDS}` in the lftp -c command strings (both full and delta sync branches) with the properly-assigned local variables. The ${{ }} expressions were already correctly placed in the env: block.

### Iteration 4

**Fixes applied:** hardcoded-credentials, script-injection

**Notes:**

Fixed hardcoded-credentials by replacing literal 'dummypassword' fallback with $(openssl rand -hex 16) runtime-generated random value. Fixed script-injection in 5 locations: (1) $INPUT_PROXY_FORWARDING_PORT in proxychains config now uses printf '%s\n' with properly quoted arguments; (2) $INPUT_SSH_OPTIONS in printf now interpolated inside a double-quoted string rather than as a separate unquoted argument; (3) ${local_path_unslash} in git diff/diff-tree commands now properly double-quoted; (4) $INPUT_SYNC_DELTA_EXCLUDES now handled via a bash array (extra_excludes) that is only populated when non-empty, preventing empty-string argument injection; (5) lftp -c command strings restructured to build via a lftp_cmd variable with paths properly escaped/quoted within the lftp command string and ftp_mirror_options/ftp_post_sync_commands only appended when non-empty.

### Iteration 5

**Fixes applied:** script-injection

**Notes:**

Fixed four unquoted shell variable expansions in action.yml's Deploy step:
1. Quoted `${git_previous_commit}` in `git cat-file -t` command (was susceptible to shell metacharacter injection via github.event.before or github.event.pull_request.base.sha).
2. Quoted `${git_previous_commit}` in `git diff --diff-filter=ACMRT` command.
3. Quoted `${git_previous_commit}` in `git diff-tree --diff-filter=D` command.
4. Quoted `${local_path_slash}` in `rsync` command (was susceptible to word splitting/glob expansion via inputs.local-path); also quoted `$HOME/files_to_upload` for consistency.
All variables are now properly double-quoted to prevent shell injection via word splitting and glob expansion.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed three script-injection vulnerabilities in hardened/action/action.yml:
1. Lines 270-271: Replaced dangerous `sed --regexp-extended 's#(.*)#realpath ... --relative-to=$local_path_unslash \1#e'` (which executes the replacement as a shell command, allowing injection via user-controlled local-path) with safe `while IFS= read -r _line; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$_line"; done` loops for both files_to_upload and files_to_delete.
2. Line 305: Changed `lftp_cmd+=" ${ftp_mirror_options}"` to `lftp_cmd+=" \"${ftp_mirror_options}\""` to prevent word-splitting/glob expansion of the user-controlled ftp-mirror-options input.
3. Lines 308 and 320: Changed both `lftp_cmd+="${ftp_post_sync_commands}"` to `lftp_cmd+="\"${ftp_post_sync_commands}\""` to prevent word-splitting/glob expansion of the user-controlled ftp-post-sync-commands input in both the full and delta sync code paths.

