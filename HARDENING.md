<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ inputs.* }}` and `${{ github.* }}` expressions into shell commands without sanitization (sub-rule a). This allows an attacker who controls input values or GitHub context values to inject arbitrary shell commands. Critical examples include:
- `input_sync=${{inputs.sync}}` — unquoted assignment, shell metacharacters flow directly into the variable
- `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — inputs injected directly into an SSH command
- `${{inputs.ftp-options}}` written into ~/.lftprc — arbitrary lftp config injection
- `${{inputs.ftp-post-sync-commands}}` interpolated inside an lftp -c "..." command string — arbitrary lftp command injection
- `${{inputs.sync-delta-excludes}}` injected into `git diff` arguments
- `git_previous_commit=${{github.event.before}}` and `git_previous_commit=${{github.event.pull_request.base.sha}}` — unquoted assignments from attacker-controlled GitHub context
- `${{github.event.head_commit.message}}` — commit message injected into an echo command
- `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)` — input injected into command substitution
- `remote_path_unslash=$(realpath --canonicalize-missing '${{inputs.remote-path}}')` — input injected into command substitution
All of these violate sub-rule (a): no `${{ ... }}` expression should appear directly inside a `run:` shell command string.

Locations:

- `action.yml:68`
- `action.yml:69`
- `action.yml:96`
- `action.yml:100`
- `action.yml:101`
- `action.yml:107`
- `action.yml:108`
- `action.yml:113`
- `action.yml:118`
- `action.yml:119`
- `action.yml:155`
- `action.yml:163`
- `action.yml:168`
- `action.yml:172`
- `action.yml:176`
- `action.yml:183`
- `action.yml:187`
- `action.yml:196`
- `action.yml:200`
- `action.yml:207`
- `action.yml:222`
- `action.yml:228`
- `action.yml:247`
- `action.yml:252`
- `action.yml:260`
- `action.yml:265`
- `action.yml:270`
- `action.yml:275`
- `action.yml:280`
- `action.yml:295`
- `action.yml:300`
- `action.yml:310`
- `action.yml:330`
- `action.yml:335`
- `action.yml:345`
- `action.yml:350`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references a mutable version tag (`@v4`) instead of a pinned 40-character commit SHA. A supply-chain attacker who compromises the `actions/upload-artifact` repository could push a malicious commit under the `v4` tag and have it execute in all workflows using this action. It should be pinned to a full SHA, e.g. `uses: actions/upload-artifact@65462800fd760344b1a7b4382951275a0abb4808 # v4`.

Locations:

- `action.yml:355`

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
1. script-injection / static-inline-injection (50+ locations): Added a comprehensive env: block to the Deploy step containing all ${{ inputs.* }} and ${{ github.* }} expressions mapped to named environment variables (INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_HOST, INPUT_REMOTE_PORT, INPUT_REMOTE_USER, INPUT_REMOTE_PASSWORD, INPUT_SSH_PRIVATE_KEY, INPUT_PROXY, INPUT_PROXY_HOST, INPUT_PROXY_PORT, INPUT_PROXY_FORWARDING_PORT, INPUT_PROXY_USER, INPUT_PROXY_PRIVATE_KEY, INPUT_LOCAL_PATH, INPUT_REMOTE_PATH, INPUT_SYNC, INPUT_SYNC_DELTA_EXCLUDES, INPUT_SSH_OPTIONS, INPUT_FTP_OPTIONS, INPUT_FTP_MIRROR_OPTIONS, INPUT_FTP_POST_SYNC_COMMANDS, INPUT_WEBHOOK, INPUT_ARTIFACTS, INPUT_DEBUG, GITHUB_REPOSITORY_VAR, GITHUB_WORKFLOW_VAR, GITHUB_JOB_VAR, GITHUB_RUN_ID_VAR, GITHUB_REF_VAR, GITHUB_EVENT_NAME_VAR, GITHUB_ACTOR_VAR, GITHUB_HEAD_COMMIT_MESSAGE_VAR, GITHUB_SHA_VAR, GITHUB_EVENT_PATH_VAR, GITHUB_EVENT_BEFORE_VAR, GITHUB_EVENT_PR_BASE_SHA_VAR, GITHUB_EVENT_INPUTS_SYNC_VAR, GITHUB_ENV_JSON_VAR, GITHUB_INPUTS_JSON_VAR). The run: block was updated to reference only these plain environment variables. The sync-delta-excludes input is now safely handled via a bash array (read -ra) to avoid word-splitting injection.
2. unpinned-uses: actions/upload-artifact@v4 pinned to actions/upload-artifact@ea165f8d65b6e75b540449e92b4886f43607fa02 # v4.

### Iteration 2

**Fixes applied:** script-injection, hardcoded-credentials

**Notes:**

Fixed all script-injection and hardcoded-credentials findings in hardened/action/action.yml:

1. hardcoded-credentials (line 155): Replaced literal 'dummypassword' with '$(openssl rand -hex 16)' to generate a random placeholder instead of a hardcoded string.

2. script-injection fixes:
   - apt-get install: Changed unquoted ${proxy_cmd} to ${proxy_cmd:+"$proxy_cmd"} so it drops out when empty and is properly quoted when present.
   - lftprc config writing: Replaced echo with printf to safely write $INPUT_FTP_OPTIONS and $INPUT_SSH_OPTIONS into the config file without shell word-splitting risks.
   - git commands: Quoted ${git_previous_commit} as "${git_previous_commit}" in git cat-file and git diff; also quoted ${local_path_unslash} as "$local_path_unslash".
   - lftp -c commands: Quoted ${local_path_unslash} and ${remote_path_unslash} within the lftp command string; used ${VAR:+"$VAR"} pattern for optional inputs $INPUT_FTP_MIRROR_OPTIONS and $INPUT_FTP_POST_SYNC_COMMANDS; used ${proxy_cmd:+"$proxy_cmd"} for the proxy command prefix.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed three script injection vulnerabilities in action.yml:
1. Converted apt_quiet string to apt_quiet_args bash array and used quoted array expansion '"${apt_quiet_args[@]}"' in apt-get commands to prevent unquoted variable expansion.
2. Replaced the dangerous 'sed ... e' flag pattern (which executes substitution results as shell commands) with a safe 'while IFS= read -r _line; do realpath ... "$local_path_unslash" "$_line"; done' loop for both files_to_upload and files_to_delete. This eliminates the arbitrary command execution risk from attacker-controlled local-path input.
3. Added double quotes around '${local_path_slash}' and '$HOME/files_to_upload' in the rsync command to prevent word-splitting and glob expansion.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed all three script injection locations in action.yml by replacing `echo "...${INPUT_VAR}..."` patterns with `printf 'format' "$INPUT_VAR"` patterns:
1. Line ~163: netrc file creation - replaced echo with printf, passing INPUT_REMOTE_HOST, INPUT_REMOTE_USER, and input_remote_password as separate printf arguments.
2. Line ~177: proxychains config creation - replaced multi-line double-quoted echo with printf, passing INPUT_PROXY_FORWARDING_PORT as a separate argument.
3. Line ~196: lftprc open command - replaced echo with printf, passing INPUT_REMOTE_PROTOCOL, INPUT_REMOTE_USER, INPUT_REMOTE_HOST, and INPUT_REMOTE_PORT as separate arguments.
In all cases, the format string is now a literal (single-quoted), so user-controlled values cannot inject shell commands by embedding double-quote characters.

