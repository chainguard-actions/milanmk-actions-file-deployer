<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.17

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.17** was hardened automatically. 54 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ inputs.* }}` and `${{ github.* }}` expressions into shell commands (rule a). This allows an attacker to inject arbitrary shell commands via crafted input values or GitHub event data. Critical examples include:
- `input_sync=${{inputs.sync}}` — unquoted, no env: indirection (line ~103)
- `input_sync_delta_includes=${{inputs.sync-delta-includes}}` — unquoted (line ~105)
- `realpath --canonicalize-missing '${{inputs.remote-path}}'` — single-quoted but still template-expanded before shell sees it (line ~97)
- `input_remote_password="${{inputs.remote-password}}"` — direct interpolation (line ~99)
- `echo "${{inputs.ssh-private-key}}" > ${key_ssh}` — private key value injected (line ~148)
- `echo "${{inputs.proxy-private-key}}" > ${key_proxy}` — proxy key injected (line ~155)
- `socks5 127.0.0.1 ${{inputs.proxy-forwarding-port}}` — injected into config (line ~161)
- `${{inputs.ftp-options}}` embedded in ~/.lftprc heredoc (line ~175)
- `echo "set sftp:connect-program /usr/bin/ssh -a -x -i ~/ssh_private_key ${{inputs.ssh-options}}"` — injected into SSH command (line ~179)
- `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — multiple inputs injected into SSH invocation (line ~196)
- `git_previous_commit=${{github.event.before}}` — unquoted (line ~228)
- `git_previous_commit=${{github.event.pull_request.base.sha}}` — unquoted (line ~230)
- `git rev-parse ${{github.sha}}^` — unquoted (line ~232)
- `${{inputs.ftp-mirror-options}}` in lftp command (line ~268)
- `${{inputs.ftp-post-sync-commands}}` in lftp command (line ~270, ~278)
- `curl ... "${{inputs.webhook}}"` — webhook URL injected (line ~83)
- `${{github.event.head_commit.message}}` passed as jq --arg value (line ~79)

Locations:

- `action.yml:69`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references a mutable tag (`@v4`) instead of a full 40-character commit SHA. This means the action could be silently updated to a malicious version without any change to this file, creating a supply-chain risk.

Locations:

- `action.yml:291`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:123`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:126`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.local-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:137`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:140`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:143`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:144`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:148`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:155`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-includes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:160`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:164`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:164`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:165`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:178`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:195`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:209`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:213`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:213`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:214`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:217`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:217`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:219`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:223`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:225`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:233`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:234`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:242`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:243`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:259`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:260`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:260`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:261`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:263`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:265`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:267`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:276`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:276`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:277`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:330`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:331`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:345`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:359`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-mirror-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:372`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:374`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:381`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:396`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:398`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses

**Notes:**

All ${{ inputs.* }} and ${{ github.* }} expressions moved from the run: block to an env: block on the Deploy step. The shell script now references them as environment variables ($INPUT_REMOTE_PROTOCOL, $INPUT_WEBHOOK, $GITHUB_SHA_VAL, etc.). List-type inputs (ssh-options, ftp-mirror-options, sync-delta-excludes) are tokenized with xargs into bash arrays to preserve argument boundaries. actions/upload-artifact@v4 pinned to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 6 script injection vulnerabilities in action.yml:

1. proxychains config (socks5 line): Replaced unquoted $INPUT_PROXY_FORWARDING_PORT inside double-quoted printf string with `printf 'socks5 127.0.0.1 %s\n' "$INPUT_PROXY_FORWARDING_PORT"` using a format string.

2. .lftprc 'open' line: Replaced `printf '%s\n' "open $INPUT_REMOTE_PROTOCOL://$INPUT_REMOTE_USER@$INPUT_REMOTE_HOST:$INPUT_REMOTE_PORT"` with `printf 'open %s://%s@%s:%s\n'` with each variable as a separate argument.

3. git diff/diff-tree commands: Quoted `${local_path_unslash}` as `"$local_path_unslash"` to prevent word-splitting and glob expansion.

4. for loop over sync-delta-includes: Replaced `for i in ${input_sync_delta_includes//,/ }` with `IFS=',' read -ra _includes <<< "${input_sync_delta_includes}"` and `for i in "${_includes[@]}"` to properly handle comma-separated values.

5. sed with 'e' flag (CRITICAL): Replaced the dangerous `sed --regexp-extended "s#(.*)#realpath --canonicalize-missing --relative-to=$local_path_unslash \1#e"` (which executes shell commands) with a safe while-read loop calling realpath directly with properly quoted arguments.

6. lftp -c command strings: Added lftp-level quoting around `${local_path_unslash}` and `${remote_path_unslash}` in the mirror command (both full-sync and delta-sync branches), and used `$post_sync_cmd` to prevent word-splitting of the post-sync commands variable.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed script-injection in both the full-sync and delta-sync branches of the Transfer files section (lines ~340 and ~360). The unsafe pattern of interpolating `$post_sync_cmd` (derived from user-controlled `$INPUT_FTP_POST_SYNC_COMMANDS`) directly into the lftp -c command string was replaced with a safer approach: the post-sync commands are written to a temporary file using `printf '%s\n' "$INPUT_FTP_POST_SYNC_COMMANDS"` (properly quoted), and lftp's `source` command is used to read from that temp file. The temp file path is controlled by the action (via mktemp), not by user input, preventing both shell-level and lftp-level injection attacks.

