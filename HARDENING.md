<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **milanmk--actions-file-deployer/1.15** was hardened automatically. 53 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ inputs.* }}` and `${{ github.* }}` expressions inside shell commands (sub-rule a). This allows an attacker who controls any of these inputs to inject arbitrary shell commands. Examples include: `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)`, `realpath '${{inputs.remote-path}}'`, `input_sync=${{inputs.sync}}` (unquoted), `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}`, `${{inputs.ftp-options}}`, `${{inputs.ftp-post-sync-commands}}`, `${{ github.event.head_commit.message }}`, `${{github.event.inputs.sync}}`. None of these values are safely routed through env vars with proper double-quoting.

Locations:

- `action.yml:74`

### unpinned-uses (severity: high)

The composite action uses `actions/upload-artifact@v4` which is pinned to a mutable tag (`v4`) rather than a full 40-character commit SHA. This is vulnerable to supply-chain attacks if the tag is moved to a malicious commit.

Locations:

- `action.yml:196`

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

Fixed all script injection issues by moving every ${{inputs.*}} and ${{github.*}} expression from the run: block into a comprehensive env: block on the Deploy step. The shell script now references all values via environment variables (INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_HOST, INPUT_SSH_PRIVATE_KEY, INPUT_PROXY_PRIVATE_KEY, INPUT_PROXY_FORWARDING_PORT, INPUT_DEBUG, INPUT_WEBHOOK, INPUT_ARTIFACTS, INPUT_FTP_OPTIONS, INPUT_FTP_MIRROR_OPTIONS, INPUT_FTP_POST_SYNC_COMMANDS, INPUT_SYNC_DELTA_EXCLUDES, INPUT_SSH_OPTIONS, GITHUB_SHA_VAL, GITHUB_EVENT_NAME_VAL, GITHUB_REPOSITORY_NAME, GITHUB_ACTOR_VAL, GITHUB_HEAD_COMMIT_MESSAGE, GITHUB_EVENT_BEFORE, GITHUB_EVENT_PR_BASE_SHA, GITHUB_EVENT_INPUTS_SYNC, GITHUB_EVENT_PATH_VAL, etc.) with proper double-quoting. Also pinned actions/upload-artifact@v4 to the full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with a # v4 comment.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script-injection findings in actions/hardened/milanmk--actions-file-deployer/1.15/action.yml:

1. INPUT_FTP_OPTIONS (line ~196): Changed `${INPUT_FTP_OPTIONS}"` to `"${INPUT_FTP_OPTIONS}""` — closes the outer double-quoted echo string before the variable, then double-quotes the variable using shell string concatenation.

2. INPUT_SSH_OPTIONS (lines ~198, 200): Changed `${INPUT_SSH_OPTIONS}"` to `""${INPUT_SSH_OPTIONS}"` in both echo commands — closes the outer double-quoted string at the space before the variable, then double-quotes the variable.

3. INPUT_SYNC_DELTA_EXCLUDES (lines ~249, 250): Changed `${INPUT_SYNC_DELTA_EXCLUDES}` to `"${INPUT_SYNC_DELTA_EXCLUDES}"` in both git diff and git diff-tree commands — these were standalone unquoted arguments, now properly double-quoted.

4. INPUT_FTP_MIRROR_OPTIONS (line ~272): Changed `${INPUT_FTP_MIRROR_OPTIONS}` to `"${INPUT_FTP_MIRROR_OPTIONS}"` inside the lftp -c command string — closes the outer double-quoted string, double-quotes the variable, and the adjacent strings are concatenated by the shell.

5. INPUT_FTP_POST_SYNC_COMMANDS (lines ~275, 283): Changed `${INPUT_FTP_POST_SYNC_COMMANDS}"` to `"${INPUT_FTP_POST_SYNC_COMMANDS}"` in both full-sync and delta-sync lftp commands — closes the outer double-quoted string, double-quotes the variable.

All fixes use shell string concatenation (adjacent quoted strings are concatenated) to properly double-quote attacker-controlled variables without breaking the surrounding shell logic.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all 6 script injection sub-issues in action.yml:

1. **apt-get unquoted ${apt_quiet} and ${proxy_cmd}**: Replaced with bash arrays (`apt_quiet_args` and `pkg_list`) expanded with `"${arr[@]}"` syntax. The `apt_quiet` string variable and its conditional assignment were removed in favor of the array approach.

2. **git cat-file unquoted ${git_previous_commit}**: Now properly quoted as `"${git_previous_commit}"`.

3. **git diff unquoted ${git_previous_commit}, ${GITHUB_SHA_VAL}, ${local_path_unslash}**: Now quoted as `"${git_previous_commit}..${GITHUB_SHA_VAL}"` and `"${local_path_unslash}"`.

4. **${proxy_cmd} as unquoted command prefix for curl**: Replaced with `proxy_cmd_arr` bash array, used as `"${proxy_cmd_arr[@]}" curl ...`.

5. **${proxy_cmd} as unquoted command prefix for lftp**: Replaced with `lftp_proxy_arr` bash array, used as `"${lftp_proxy_arr[@]}" lftp -f "${lftp_script}"`.

6. **Unquoted ${local_path_unslash}/${remote_path_unslash} in lftp mirror, and ${INPUT_FTP_MIRROR_OPTIONS}/${INPUT_FTP_POST_SYNC_COMMANDS} injected into lftp -c strings**: Replaced `lftp -c "..."` with `lftp -f script_file` approach. The lftp script is built using `printf` with proper quoting for path variables. Post-sync commands are written to the script file with `printf '%s\n'` only when non-empty, keeping them as lftp-level commands rather than shell-level injection.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed three script injection vulnerabilities in action.yml:
1. Replaced two dangerous `sed --regexp-extended 's#(.*)#realpath ... --relative-to=$local_path_unslash \1#e'` commands (lines 232-233) with safe `while IFS= read -r line` loops that call `realpath` directly with properly quoted arguments. The sed 'e' flag executes the replacement as a shell command, and the unquoted $local_path_unslash (derived from inputs.local-path) allowed arbitrary command injection.
2. Fixed the `rsync` command (line 238) by quoting `${local_path_slash}` as `"${local_path_slash}"` to prevent word-splitting and glob expansion on the attacker-controlled value.

### Iteration 1

**Fixes applied:** hardcoded-credentials

**Notes:**

Replaced the hardcoded literal 'dummypassword' placeholder in action.yml (line 148) with a runtime-generated random value using `$(openssl rand -hex 16)`. The placeholder is needed because lftp requires a non-empty password field in ~/.netrc even when SSH key authentication is used. Using a random value at runtime eliminates the hardcoded credential pattern while preserving functional behavior.

