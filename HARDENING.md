<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions into shell commands without routing them through env: variables, violating rule (a). An attacker who controls any of these inputs (e.g. via a calling workflow) can inject arbitrary shell commands. Representative violations include:
- `input_sync=${{inputs.sync}}` — unquoted, no env: indirection
- `input_sync=${{github.event.inputs.sync}}` — unquoted
- `git_previous_commit=${{github.event.before}}` — unquoted shell assignment
- `git_previous_commit=${{github.event.pull_request.base.sha}}` — unquoted
- `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — multiple unquoted inputs injected into an SSH command
- `${{inputs.ftp-post-sync-commands}}` injected directly into an lftp -c string (twice)
- `${{inputs.ftp-mirror-options}}` injected into an lftp -c string
- `${{inputs.ssh-options}}` appended to SSH connect-program config
- `${{inputs.remote-host}}`, `${{inputs.remote-user}}`, `${{inputs.remote-port}}`, `${{inputs.remote-protocol}}` interpolated into shell strings
- `${{github.event.head_commit.message}}` passed as a jq --arg value (commit messages can contain shell metacharacters)
All of these must be moved to env: variables and the shell expansions must be double-quoted.

Locations:

- `action.yml:68`
- `action.yml:75`
- `action.yml:77`
- `action.yml:100`
- `action.yml:102`
- `action.yml:175`
- `action.yml:177`
- `action.yml:179`
- `action.yml:181`
- `action.yml:225`
- `action.yml:248`
- `action.yml:250`
- `action.yml:280`
- `action.yml:282`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v4`, which uses a mutable version tag rather than a pinned 40-character commit SHA. This means the action could be silently replaced with a malicious version without any change to this file. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:310`

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

Fixed all script injection findings by adding an env: block to the Deploy step that maps all ${{ inputs.* }} and ${{ github.* }} expressions to named environment variables (INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_HOST, INPUT_REMOTE_USER, INPUT_REMOTE_PASSWORD, INPUT_SSH_PRIVATE_KEY, INPUT_PROXY, INPUT_PROXY_HOST, INPUT_PROXY_PORT, INPUT_PROXY_FORWARDING_PORT, INPUT_PROXY_USER, INPUT_PROXY_PRIVATE_KEY, INPUT_LOCAL_PATH, INPUT_REMOTE_PATH, INPUT_SYNC, INPUT_SYNC_DELTA_EXCLUDES, INPUT_SSH_OPTIONS, INPUT_FTP_OPTIONS, INPUT_FTP_MIRROR_OPTIONS, INPUT_FTP_POST_SYNC_COMMANDS, INPUT_WEBHOOK, INPUT_ARTIFACTS, INPUT_DEBUG, and GITHUB_REPOSITORY_VAR, GITHUB_WORKFLOW_VAR, GITHUB_JOB_VAR, GITHUB_RUN_ID_VAR, GITHUB_REF_VAR, GITHUB_EVENT_NAME_VAR, GITHUB_ACTOR_VAR, GITHUB_SHA_VAR, GITHUB_EVENT_PATH_VAR, GITHUB_HEAD_COMMIT_MESSAGE, GITHUB_EVENT_BEFORE, GITHUB_EVENT_PR_BASE_SHA, GITHUB_EVENT_INPUTS_SYNC, GITHUB_TOJON_ENV, GITHUB_TOJON_INPUTS). The run: block now uses only $VAR_NAME style references throughout. Also pinned actions/upload-artifact@v4 to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02 # v4.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 7 script injection vulnerabilities in action.yml:
1. netrc line: replaced `echo "machine $INPUT_REMOTE_HOST login $INPUT_REMOTE_USER ..."` with `printf 'machine %s login %s password %s\n' "$INPUT_REMOTE_HOST" "$INPUT_REMOTE_USER" ...` to prevent $() and backtick evaluation.
2. lftprc $INPUT_FTP_OPTIONS: separated from static config string and appended with `printf '%s\n' "$INPUT_FTP_OPTIONS"`.
3. lftprc $INPUT_SSH_OPTIONS: replaced echo with `printf 'set sftp:connect-program ... %s\n' "$INPUT_SSH_OPTIONS"`.
4. lftprc open command: replaced echo with `printf 'open %s://%s@%s:%s\n' "$INPUT_REMOTE_PROTOCOL" "$INPUT_REMOTE_USER" "$INPUT_REMOTE_HOST" "$INPUT_REMOTE_PORT"`.
5. git diff $INPUT_SYNC_DELTA_EXCLUDES: tokenized with xargs into a bash array using the guarded xargs/read-loop idiom, then expanded as `"${sync_delta_excludes[@]}"`.
6-7. lftp $INPUT_FTP_MIRROR_OPTIONS and $INPUT_FTP_POST_SYNC_COMMANDS: rewrote both full and delta sync lftp invocations to use `lftp -f <tempfile>` instead of `lftp -c "..."`, writing commands to the temp file with printf format strings to prevent shell evaluation of user-controlled content.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all unquoted shell variable expansions in action.yml:
1. ${proxy_cmd} in apt-get install: changed to ${proxy_cmd:+"${proxy_cmd}"} to avoid passing empty string as argument
2. ${proxy_cmd} in proxy IP check and both lftp invocations: same conditional expansion fix
3. ${local_path_unslash} in git diff and git diff-tree: now double-quoted as "${local_path_unslash}"
4. ${git_previous_commit} in git cat-file, git diff, and git diff-tree: now double-quoted as "${git_previous_commit}"
5. $INPUT_PROXY_FORWARDING_PORT in proxychains config: changed from echo with embedded variable to printf with %s format specifier and properly quoted argument
6. $INPUT_FTP_MIRROR_OPTIONS was already double-quoted in the current file (fixed in a previous iteration)

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed two script-injection findings in action.yml:

1. **sed #e flag injection (lines 218-219)**: Replaced `sed --in-place --regexp-extended "s#(.*)#realpath --canonicalize-missing --relative-to=$local_path_unslash \1#e"` with a `while IFS= read -r _fpath; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$_fpath"; done` loop. This eliminates the dangerous `#e` flag that executed the sed replacement as a shell command with user-controlled data.

2. **printf with argument-list inputs (lines 163, 165, 167, 232, 241)**:
   - SSH options: Tokenized `$INPUT_SSH_OPTIONS` into a `ssh_opts` bash array using the xargs pattern, then used `printf ' %s' "${ssh_opts[@]}"` to safely append each option as a separate token to the lftprc config line.
   - FTP mirror options: Tokenized `$INPUT_FTP_MIRROR_OPTIONS` into a `mirror_opts` bash array using the xargs pattern, then built the mirror command using `{ printf 'mirror ...'; printf ' %s' "${mirror_opts[@]}"; printf ' %s %s;\n' ... }` to keep each token separate.
   - FTP post-sync commands: Already quoted with `printf '%s\n' "$INPUT_FTP_POST_SYNC_COMMANDS"` — the format string is a literal and the variable is the sole argument, so no change needed.

### Iteration 5

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted shell variable expansion in the rsync command at line 246 of action.yml. Changed `rsync --verbose --files-from=$HOME/files_to_upload ${local_path_slash} ~/transfer_files/` to `rsync --verbose --files-from="$HOME/files_to_upload" "${local_path_slash}" ~/transfer_files/`. The `${local_path_slash}` variable is derived from user-controlled input `inputs.local-path` and must be double-quoted to prevent shell metacharacter injection (spaces, globs, semicolons, etc.).

