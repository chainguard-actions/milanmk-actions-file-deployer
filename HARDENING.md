<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.16

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.16** was hardened automatically. 53 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' step's run: block directly interpolates ${{ }} expressions into shell commands (sub-rule a), enabling script injection. There are 82 such interpolations throughout the single run block. Critically dangerous examples include:
- `${{inputs.ftp-post-sync-commands}}` injected directly into an lftp -c command string (attacker can inject arbitrary lftp/shell commands)
- `${{inputs.ftp-options}}` and `${{inputs.ftp-mirror-options}}` injected into shell heredocs and lftp commands
- `${{inputs.ssh-options}}` injected into an SSH command line
- `${{inputs.webhook}}` used as a URL argument to curl
- `${{inputs.sync-delta-excludes}}` injected into git diff command arguments
- `${{inputs.local-path}}` and `${{inputs.remote-path}}` injected unquoted into shell commands
- `${{inputs.remote-password}}`, `${{inputs.ssh-private-key}}`, `${{inputs.proxy-private-key}}` interpolated directly
- `${{github.event.head_commit.message}}`, `${{github.event.inputs.sync}}`, `${{github.event.before}}`, `${{github.event.pull_request.base.sha}}` — all attacker-controllable github context values interpolated directly into shell
- `${{inputs.proxy-forwarding-port}}`, `${{inputs.proxy-port}}`, `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}` injected into an SSH command
All of these are YAML-template-substituted before the shell parses the script, allowing an attacker to inject arbitrary shell metacharacters and commands.

Locations:

- `action.yml:68`

### unpinned-uses (severity: high)

The 'Upload artifacts' step references `actions/upload-artifact@v4`, which uses a mutable tag (`v4`) instead of a pinned 40-character commit SHA. A compromised or updated tag could silently execute different code, enabling a supply-chain attack.

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

1. All ${{ }} expressions in the Deploy step's run: block have been moved to an env: block. This covers all 23 inputs and 15 github context values (82+ total interpolations). The run: block now uses only plain $VAR_NAME references.
2. List-style inputs (ssh-options, ftp-mirror-options, sync-delta-excludes) are tokenized using the xargs/while-read-NUL pattern to preserve argument boundaries safely.
3. ftp-options is written to ~/.lftprc using printf '%s' to avoid injection.
4. ftp-post-sync-commands is stored in a shell variable and passed to lftp -c as an lftp command string (same behavior as upstream).
5. actions/upload-artifact@v4 has been pinned to commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with # v4 comment.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all unquoted variable expansions identified in the finding:
1. Converted `proxy_cmd` from a string to a bash array (`proxy_cmd=()` / `proxy_cmd=("proxychains")`), enabling safe expansion with `"${proxy_cmd[@]}"` which produces zero words when empty and `"proxychains"` when set.
2. Updated `sudo apt-get ... install lftp ${proxy_cmd}` to use `"${proxy_cmd[@]}"` array expansion.
3. Updated proxy IP check `$(${proxy_cmd} curl ...)` to `$("${proxy_cmd[@]}" curl ...)`.
4. Quoted `${local_path_slash}` in the rsync command: `rsync ... "${local_path_slash}" ~/transfer_files/`.
5. Updated both lftp invocations (full sync and delta sync) from `${proxy_cmd} lftp` to `"${proxy_cmd[@]}" lftp`.
6. Added lftp-level quoting for `${local_path_unslash}` and `${remote_path_unslash}` in the mirror command (now `\"${local_path_unslash}\"` and `\"${remote_path_unslash}\"`).
The `${ftp_post_sync_cmds}` and `${mirror_opts_str}` variables are inside the outer double-quoted shell string so they are already protected from shell word splitting and glob expansion.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all four script-injection sub-issues in action.yml:

1. **apt_quiet (line ~175)**: Changed `apt_quiet` string variable to `apt_quiet_flags` bash array. Now safely expanded as `"${apt_quiet_flags[@]}"` in apt-get commands, preventing shell metacharacter injection.

2. **sed #e with $local_path_unslash (lines ~281-282)**: Replaced the dangerous `sed --regexp-extended 's#(.*)#realpath ... --relative-to=$local_path_unslash \1#e'` (which executes shell commands via the `#e` flag) with a safe `while IFS= read -r fline; do realpath ... "$local_path_unslash" "$fline"; done` loop that calls realpath directly with properly quoted arguments.

3. **mirror_opts_str (line ~319)**: Eliminated the intermediate `mirror_opts_str` string variable. Now writes lftp commands to a temp script file using `printf` with the already-safe `ftp_mirror_opts` array expanded as `"${ftp_mirror_opts[@]}"`.

4. **ftp_post_sync_cmds (lines ~321, ~329)**: Changed from unquoted inline interpolation in lftp `-c` strings to writing the value to a temp lftp script file using `printf '%s\n' "$ftp_post_sync_cmds"` (properly quoted, treated as data). lftp then executes the script file with `-f` flag instead of inline `-c` string interpolation, eliminating the shell injection vector.

