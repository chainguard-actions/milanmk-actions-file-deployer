<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.15** was hardened automatically. 53 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Sub-rule (a): The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ }} expressions into shell commands without any sanitization. This allows an attacker (or a calling workflow) to inject arbitrary shell commands. Highly dangerous examples include:
- `input_sync=${{inputs.sync}}` — unquoted assignment, shell metacharacters in the value are parsed
- `input_sync=${{github.event.inputs.sync}}` — attacker-controlled via workflow_dispatch
- `realpath --canonicalize-missing '${{inputs.remote-path}}'` — injected into a shell argument
- `echo "${{inputs.ftp-options}}" > ~/.lftprc` — arbitrary lftp config injection
- `echo "set sftp:connect-program /usr/bin/ssh -a -x -i ~/ssh_private_key ${{inputs.ssh-options}}"` — ssh option injection
- `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — unquoted SSH arguments
- `lftp -c "... ${{inputs.ftp-mirror-options}} ..."` and `lftp -c "... ${{inputs.ftp-post-sync-commands}}"` — arbitrary lftp command injection
- `git diff ... ${{inputs.sync-delta-excludes}}` — arbitrary git argument injection
- `${{github.event.before}}`, `${{github.event.pull_request.base.sha}}`, `${{github.sha}}^` — github context values used unquoted in shell
- `${{github.event_path}}` passed directly to `cat`
All of these ${{ }} interpolations happen before the shell ever sees the string, enabling command injection.

Locations:

- `action.yml:68`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' uses `actions/upload-artifact@v4`, which is a mutable tag reference rather than a pinned 40-character commit SHA. This means the action could be silently updated to a different (potentially malicious) version without the consuming workflow's knowledge. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

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

1. Moved all ${{ }} expressions from the Deploy step's run: block into an env: block. All inputs and github context values are now set as environment variables (INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_HOST, INPUT_REMOTE_PORT, INPUT_REMOTE_USER, INPUT_REMOTE_PASSWORD, INPUT_SSH_PRIVATE_KEY, INPUT_PROXY, INPUT_PROXY_HOST, INPUT_PROXY_PORT, INPUT_PROXY_FORWARDING_PORT, INPUT_PROXY_USER, INPUT_PROXY_PRIVATE_KEY, INPUT_LOCAL_PATH, INPUT_REMOTE_PATH, INPUT_SYNC, INPUT_SYNC_DELTA_EXCLUDES, INPUT_SSH_OPTIONS, INPUT_FTP_OPTIONS, INPUT_FTP_MIRROR_OPTIONS, INPUT_FTP_POST_SYNC_COMMANDS, INPUT_WEBHOOK, INPUT_ARTIFACTS, INPUT_DEBUG, and all GITHUB_* context values). The run: block uses $VAR_NAME shell references instead. List-style inputs (sync-delta-excludes, ssh-options) use xargs-based tokenization into bash arrays. 2. Pinned actions/upload-artifact@v4 to full SHA: actions/upload-artifact@ea165f8d65b6e75b540449e92b4886f43607fa02 # v4

### Iteration 2

**Fixes applied:** hardcoded-credentials, script-injection

**Notes:**

Fixed all four findings in action.yml:
1. hardcoded-credentials (line 155): Replaced literal 'dummypassword' with 'openssl rand -hex 16' to generate a random placeholder at runtime.
2. script-injection (line 233, $INPUT_FTP_OPTIONS): Split the static lftprc config from the user-controlled value; the static block is written with echo, then INPUT_FTP_OPTIONS is appended separately with properly quoted 'printf "%s\n" "$INPUT_FTP_OPTIONS"'.
3. script-injection (lines 237, 239, ${ssh_opts_args[*]}): Replaced unquoted [*] expansion inside double-quoted echo strings with 'printf " %s" "${ssh_opts_args[@]}"' which safely writes each array element.
4. script-injection (lines 330, 333, 341, ${ftp_mirror_opts} and ${ftp_post_sync}): Replaced the lftp -c "..." inline string approach (which allowed shell metacharacter injection) with writing lftp commands to a mktemp file using printf and executing with 'lftp -f "$lftp_script"'. User-controlled ftp_post_sync is written with 'printf "%s\n" "$ftp_post_sync"' (properly quoted).

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed three script injection vulnerabilities in action.yml:
1. Quoted '${local_path_unslash}' in both git diff and git diff-tree commands to prevent word-splitting and glob expansion on attacker-controlled input.
2. Used 'printf %q' to shell-quote '$local_path_unslash' before interpolating it into the sed expression that uses the /e flag (which executes the replacement as a shell command). This prevents arbitrary command injection via the local-path input.
3. Replaced the unquoted '$ftp_mirror_opts' variable (used in 'printf " %s" $ftp_mirror_opts') with a properly tokenized array 'ftp_mirror_opts_args' built using the xargs/while-read-NUL pattern, then expanded safely as '"${ftp_mirror_opts_args[@]}"'.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed all 8 script injection locations in action.yml:
1. Introduced proxy_cmd_arr=() / proxy_cmd_arr=("proxychains") alongside proxy_cmd for safe array-based command prefixing.
2. apt-get install: replaced unquoted ${proxy_cmd} with an apt_extra_pkgs array expanded as "${apt_extra_pkgs[@]}".
3. curl in proxy setup: replaced unquoted ${proxy_cmd} with "${proxy_cmd_arr[@]}".
4. git cat-file: quoted ${git_previous_commit} as "${git_previous_commit}".
5. git diff and git diff-tree: quoted ${git_previous_commit} as "${git_previous_commit}" and also quoted $GITHUB_SHA_VAL.
6. rsync: quoted ${local_path_slash} as "${local_path_slash}".
7-8. Both lftp invocations (full-sync and delta-sync): replaced unquoted ${proxy_cmd} with "${proxy_cmd_arr[@]}".
All values derived from user-controlled inputs are now properly quoted or handled via arrays, preventing shell metacharacter injection.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed two script-injection findings in action.yml:
1. apt_quiet unquoted expansion (line ~237): Converted `apt_quiet` string variable to a bash array `apt_quiet_args` (holding `(--quiet --quiet)` or `()`) and expanded it safely with `"${apt_quiet_args[@]}"` in both apt-get calls. This avoids word-splitting while correctly passing multiple flags.
2. sed /e flag injection (lines 237-238): Replaced the dangerous `sed --regexp-extended 's#(.*)#realpath ... ${local_path_unslash_quoted} \1#e'` pattern (which executes the replacement as a shell command) with a safe `while IFS= read -r filepath; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$filepath"; done` loop that calls realpath directly with properly quoted arguments, eliminating the shell command injection risk.

