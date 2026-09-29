<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.16

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.16** was hardened automatically. 53 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions into shell commands without routing them through env: variables or quoting. This allows arbitrary shell command injection by any caller of the action. Critical examples include:
- (a) `input_sync=${{inputs.sync}}` — unquoted, unguarded direct interpolation into shell assignment
- (a) `git_previous_commit=${{github.event.before}}` — unquoted github context value assigned in shell
- (a) `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — multiple inputs injected directly into an ssh command
- (a) `${{inputs.ftp-post-sync-commands}}` injected directly into lftp -c command strings (appears twice)
- (a) `${{inputs.ftp-mirror-options}}` injected into lftp mirror command
- (a) `${{inputs.ftp-options}}` written into ~/.lftprc config file via heredoc
- (a) `${{inputs.ssh-options}}` appended to sftp:connect-program config
- (a) `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)` — inputs.local-path interpolated into command substitution
- (a) `remote_path_unslash=$(realpath --canonicalize-missing '${{inputs.remote-path}}')` — inputs.remote-path interpolated into command
- (a) Multiple github.* context values (github.event.head_commit.message, github.actor, github.ref, etc.) interpolated into jq --arg arguments inside the send_webhook function
All of these are sub-rule (a) violations: ${{ ... }} expressions appear directly inside run: shell command strings.

Locations:

- `action.yml:68`
- `action.yml:84`
- `action.yml:87`
- `action.yml:93`
- `action.yml:96`
- `action.yml:100`
- `action.yml:107`
- `action.yml:155`
- `action.yml:175`
- `action.yml:185`
- `action.yml:199`
- `action.yml:210`
- `action.yml:237`
- `action.yml:243`
- `action.yml:258`
- `action.yml:277`
- `action.yml:283`
- `action.yml:310`
- `action.yml:320`
- `action.yml:327`
- `action.yml:340`
- `action.yml:358`
- `action.yml:362`

### unpinned-uses (severity: high)

The 'Upload artifacts' step uses `actions/upload-artifact@v4`, which is a mutable tag reference rather than a pinned 40-character SHA commit hash. This means the action could be silently updated to a different (potentially malicious) version without any change to this file, creating a supply-chain risk.

Locations:

- `action.yml:368`

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

Rewrote action.yml to fix all script injection findings: moved all 36 ${{ inputs.* }} and ${{ github.* }} expressions from the run: shell block into a comprehensive env: block on the Deploy step. The shell script now references only plain environment variables. List-style inputs (sync-delta-excludes, ftp-mirror-options) are tokenized with xargs/while-read-d-null to preserve argument boundaries. Pinned actions/upload-artifact@v4 to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script-injection vectors in action.yml:

1. $INPUT_SSH_OPTIONS: Changed printf '%s\n' "set sftp:connect-program ... $INPUT_SSH_OPTIONS" to printf 'set sftp:connect-program ... %s\n' "$INPUT_SSH_OPTIONS" — variable is now a printf argument, not embedded in a double-quoted string subject to shell expansion.

2. $INPUT_REMOTE_PROTOCOL/$INPUT_REMOTE_USER/$INPUT_REMOTE_HOST/$INPUT_REMOTE_PORT: Changed printf '%s\n' "open $VAR://$VAR@$VAR:$VAR" to printf 'open %s://%s@%s:%s\n' "$VAR" "$VAR" "$VAR" "$VAR" — each variable is a separate printf argument.

3. ${post_sync_cmds} in lftp -c (both full-sync and delta-sync branches): Replaced lftp -c "...${post_sync_cmds}" with writing lftp commands to a mktemp file and using lftp -f "$lftp_script". Post-sync commands written with printf '%s\n' "$INPUT_FTP_POST_SYNC_COMMANDS".

4. ${mirror_opts[*]} in lftp -c: Same lftp script file approach — mirror options written with a for loop using printf ' %s' "$_opt" for each tokenized option.

5. $local_path_unslash in sed #e (command execution): Replaced sed --regexp-extended "s#(.*)#realpath ... --relative-to=$local_path_unslash \1#e" with a safe while-loop: while IFS= read -r _line; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$_line"; done — eliminates the shell command execution via sed's #e flag entirely.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all unquoted shell variable expansions in the Deploy step:
1. Quoted `${git_previous_commit}` in git cat-file (-t), git diff, and git diff-tree commands
2. Quoted `${local_path_unslash}` in git diff and git diff-tree path arguments
3. Quoted `${local_path_slash}` in the rsync command
4. Rewrote the proxychains config printf to use a `%s` format specifier with `"$INPUT_PROXY_FORWARDING_PORT"` as a separate quoted argument instead of embedding it unquoted inside a double-quoted string
5. Changed `${proxy_cmd}` in apt-get install to `${proxy_cmd:+"$proxy_cmd"}` to safely handle the empty/non-empty cases

