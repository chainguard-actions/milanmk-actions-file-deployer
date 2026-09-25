<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions into shell commands (rule a). These expressions are expanded by the GitHub Actions template engine before the shell ever sees them, allowing an attacker who controls input values to inject arbitrary shell commands. Critical examples include:
- `input_sync=${{inputs.sync}}` — unquoted, no env: indirection
- `input_sync=${{github.event.inputs.sync}}` — unquoted
- `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — multiple unquoted inputs injected directly into an SSH command
- `${{inputs.ftp-options}}`, `${{inputs.ftp-mirror-options}}`, `${{inputs.ftp-post-sync-commands}}` — injected verbatim into lftp -c command strings
- `echo "set sftp:connect-program /usr/bin/ssh -a -x ${{inputs.ssh-options}}"` — injected into SSH config
- `git diff ... ${{inputs.sync-delta-excludes}}` — injected into git diff arguments
- `git_previous_commit=${{github.event.before}}` — unquoted git SHA from event payload
- `cat ${{github.event_path}}` — unquoted path
- `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)` and `realpath ... '${{inputs.remote-path}}'` — path inputs interpolated directly
- `${{inputs.remote-password}}`, `${{inputs.remote-host}}`, `${{inputs.remote-user}}`, `${{inputs.remote-port}}`, `${{inputs.remote-protocol}}`, `${{inputs.proxy-private-key}}`, `${{inputs.proxy-forwarding-port}}`, `${{inputs.webhook}}`, `${{inputs.artifacts}}`, `${{inputs.debug}}` — all interpolated directly throughout the script
All of these must be moved to env: variables and then double-quoted in the shell script.

Locations:

- `action.yml:68`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v4`, which uses a mutable version tag rather than a pinned 40-character commit SHA. A tag can be moved by the upstream repository owner (or a compromised account) to point to a different, potentially malicious commit, enabling a supply-chain attack. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:261`

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

Fixed all script injection findings by moving all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block into the step's env: block. Created 38 environment variables covering all inputs (remote-protocol, remote-host, remote-port, remote-user, remote-password, ssh-private-key, proxy, proxy-host, proxy-port, proxy-forwarding-port, proxy-user, proxy-private-key, local-path, remote-path, sync, sync-delta-excludes, ssh-options, ftp-options, ftp-mirror-options, ftp-post-sync-commands, webhook, artifacts, debug) and all github context values (repository, workflow, job, run_id, ref, event_name, actor, event.head_commit.message, sha, event.before, event.pull_request.base.sha, event_path, event.inputs.sync, toJSON(env), toJSON(inputs)). The shell script now references these as $VAR_NAME. Also pinned actions/upload-artifact@v4 to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02 # v4.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 7 script-injection issues in action.yml:

1. ${proxy_cmd} in apt-get install (line 148): Changed to ${proxy_cmd:+"${proxy_cmd}"} to safely handle empty/non-empty cases without passing empty argument.

2. $INPUT_FTP_OPTIONS in echo to ~/.lftprc (line 172): Separated static config from user options. Static config written with echo, then user options appended with `printf '%s\n' "$INPUT_FTP_OPTIONS" >> ~/.lftprc`.

3. $INPUT_SSH_OPTIONS in echo to ~/.lftprc (lines 174/176): Changed from unquoted echo to `printf 'set sftp:connect-program ... %s\n' "$INPUT_SSH_OPTIONS"` with proper quoting.

4. $INPUT_SYNC_DELTA_EXCLUDES in git diff/diff-tree (lines 218/219): Tokenized into a bash array using xargs (with guard for empty value), then expanded as "${sync_delta_excludes[@]}" in git commands.

5. ${git_previous_commit} in git cat-file (line 216): Changed to "${git_previous_commit}".

6. $INPUT_FTP_MIRROR_OPTIONS in lftp -c (line 243): Restructured to use printf to build the lftp command string with "$INPUT_FTP_MIRROR_OPTIONS" as a properly quoted %s argument.

7. $INPUT_FTP_POST_SYNC_COMMANDS in lftp -c (lines 243/245): Same printf restructuring with "$INPUT_FTP_POST_SYNC_COMMANDS" properly quoted.

Additionally fixed ${proxy_cmd} as command prefix in lftp calls and proxy IP check using ${proxy_cmd:+"${proxy_cmd}"} pattern.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed four unquoted variable expansion vulnerabilities in the 'Deploy' run block:

1. Quoted `${local_path_unslash}` in the `git diff` command (was unquoted, allowing word splitting and glob expansion).
2. Quoted `${local_path_unslash}` in the `git diff-tree` command (same issue).
3. Replaced the dangerous `sed --regexp-extended "s#(.*)#realpath --canonicalize-missing --relative-to=$local_path_unslash \1#e"` pattern with a safe `while IFS= read -r _line; do realpath --canonicalize-missing --relative-to="${local_path_unslash}" "${_line}"; done` loop. The original `#e` sed flag executes the substitution result as a shell command, making unquoted `$local_path_unslash` a direct command injection vector. The replacement avoids shell execution entirely.
4. Quoted `${local_path_slash}` and `$HOME/files_to_upload` in the `rsync` command.

The sed `#e` replacement was the most critical fix — it eliminated a direct arbitrary command execution path controlled by the `inputs.local-path` value.

### Iteration 4

**Fixes applied:** hardcoded-credentials

**Notes:**

Replaced the hardcoded placeholder password 'dummypassword' at action.yml line 148 with a runtime-generated random value: `$(openssl rand -hex 16)`. This eliminates the literal credential value while preserving the functional requirement of having a non-empty placeholder in the .netrc file when no real password is provided (SSH key auth scenario). openssl is available on the Ubuntu runners this action targets.

### Iteration 5

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted ${apt_quiet} variable in apt-get commands at line 175 of action.yml. Changed `sudo apt-get ${apt_quiet} update && sudo apt-get ${apt_quiet} --no-install-recommends ...` to use `${apt_quiet:+"${apt_quiet}"}` conditional expansion pattern. This double-quotes the value when non-empty (preventing word splitting/glob expansion) and produces no argument when empty (debug mode), consistent with the existing pattern used for proxy_cmd in the same line.

