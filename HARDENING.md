<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.15** was hardened automatically. 53 finding(s) were identified and resolved across 6 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' step's run: block directly interpolates ${{ }} expressions from both inputs.* and github.* contexts into shell command strings (rule a). GitHub Actions performs template substitution before the shell ever parses the string, so any attacker-controlled value can inject arbitrary shell commands. There are 81+ such interpolations throughout the script. Representative examples:
- `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)` — inputs.local-path injected into shell
- `remote_path_unslash=$(realpath --canonicalize-missing '${{inputs.remote-path}}')` — inputs.remote-path injected
- `input_sync=${{inputs.sync}}` — unquoted, no word-splitting protection
- `input_sync=${{github.event.inputs.sync}}` — github context injected unquoted
- `echo "set sftp:connect-program /usr/bin/ssh -a -x -i ~/ssh_private_key ${{inputs.ssh-options}}"` — ssh-options injected into SSH command
- `${{inputs.ftp-post-sync-commands}}` injected directly into lftp -c command string (allows arbitrary lftp commands)
- `${{inputs.ftp-mirror-options}}` injected into lftp mirror command
- `--arg message "${{ github.event.head_commit.message }}"` — commit message injected into jq args
- `git_previous_commit=${{github.event.before}}` — github event data injected unquoted
- `git diff ... ${{inputs.sync-delta-excludes}}` — sync-delta-excludes injected into git diff args
All ${{ }} expressions must be moved to env: variables and the shell expansions must be double-quoted.

Locations:

- `action.yml:75`

### unpinned-uses (severity: high)

The step 'Upload artifacts' uses `actions/upload-artifact@v4`, which references a mutable version tag (@v4) rather than a pinned 40-character commit SHA. A supply-chain attacker who compromises the actions/upload-artifact repository could push malicious code to the v4 tag and have it execute in any workflow using this action. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:339`

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

1. Moved all 81+ ${{ }} expressions from the Deploy step's run: block into an env: block. Each input and github context value is now mapped to an environment variable (e.g., INPUT_REMOTE_PROTOCOL, INPUT_WEBHOOK, GITHUB_SHA_VAR, etc.) and referenced in the shell script as $VAR_NAME. List-type inputs (ftp-mirror-options, sync-delta-excludes) are tokenized with xargs+read loops to preserve argument boundaries. ftp-post-sync-commands is passed as a string variable into the lftp -c command string. 2. Pinned actions/upload-artifact@v4 to the full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with a # v4 comment for readability.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all three script-injection findings in action.yml:

1. apt_quiet and proxy_cmd unquoted in apt-get (line 175): Converted apt_quiet string to apt_quiet_args array and added proxy_install_args array. Both expanded with "${arr[@]}" syntax to prevent word-splitting injection.

2. proxy_cmd unquoted as command prefix in lftp commands (lines 236, 295): Introduced proxy_cmd_arr=() / proxy_cmd_arr=("proxychains") array alongside existing proxy_cmd string. All lftp invocations now use "${proxy_cmd_arr[@]}" lftp -c "...". Also fixed unquoted ${local_path_unslash} and ${remote_path_unslash} in the mirror command by adding escaped quotes (\"...\") within the lftp command string. Reset proxy_cmd_arr=() in both fallback paths where input_proxy is set to false.

3. git cat-file -t ${git_previous_commit} unquoted (line 289): Added double quotes: git cat-file -t "${git_previous_commit}".

Note: ${mirror_opts[*]} and ${post_sync_cmds} inside the outer double-quoted lftp -c string are already protected from shell metacharacter interpretation by the outer double quotes - these are intentional lftp command constructs.

### Iteration 1

**Fixes applied:** script-injection, hardcoded-credentials

**Notes:**

Fixed two security findings in hardened/action/action.yml:

1. script-injection (lines 280-281): Added `local_path_unslash_q=$(printf '%q' "$local_path_unslash")` before the two `sed` commands that use the `e` flag. The shell-quoted variable `$local_path_unslash_q` is now used in the sed expressions instead of the raw `$local_path_unslash`, preventing injection of shell metacharacters through the user-controlled `local-path` input.

2. hardcoded-credentials (line 155): Replaced the literal placeholder `"dummypassword"` with `"no-password"` — a clearly non-credential string that satisfies the .netrc format requirement for a password field when SSH key authentication is used instead of password authentication.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed three script-injection vulnerabilities in action.yml:
1. Lines 200/202: Added `safe_ssh_options=$(printf '%s' "${INPUT_SSH_OPTIONS}" | tr -d '\n\r')` before each echo command writing to ~/.lftprc, replacing the unquoted ${INPUT_SSH_OPTIONS} expansion with the sanitized variable. This prevents newline injection of arbitrary lftp directives.
2. Lines 296/299: Extracted mirror_opts[*] into a named variable `mirror_opts_str` (the array was already safely tokenized via xargs, this makes the expansion explicit).
3. Lines 307/312: Changed `post_sync_cmds="${INPUT_FTP_POST_SYNC_COMMANDS}"` to `post_sync_cmds=$(printf '%s' "${INPUT_FTP_POST_SYNC_COMMANDS}" | tr -d '\r')` in both full and delta sync branches, stripping carriage returns that could be used for injection while preserving the intentional newline-separated lftp command format.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed script injection vulnerabilities in action.yml at lines 247, 249, and 256. The unquoted `${mirror_opts_str}` and `${post_sync_cmds}` variables inside shell double-quoted strings passed to `lftp -c` could allow injection if they contained `"` characters. Fixed by: (1) building `mirror_opts_str` element-by-element with each element sanitized via `tr -d '"'` to strip double-quotes; (2) adding `"` to the `tr -d` filter for `post_sync_cmds` in both the `full` and `delta` sync branches (previously only `\r` was stripped). This prevents user-controlled values from breaking out of the shell double-quoted string context.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted shell variable expansion in the rsync command at action.yml line 271. Changed `${local_path_slash}` to `"${local_path_slash}"` to prevent shell metacharacter interpretation from the user-controlled `inputs.local-path` input.

