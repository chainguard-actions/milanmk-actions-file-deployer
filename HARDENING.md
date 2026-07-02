<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 54 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The single `run:` step in action.yml directly interpolates dozens of `${{ }}` expressions into shell commands, violating rule (a). This allows an attacker to inject arbitrary shell commands via controlled inputs or GitHub event data.

Key violations include:

(a) Direct expression interpolation in shell:
- `input_sync=${{inputs.sync}}` — unquoted, no surrounding quotes (line ~107)
- `input_sync_delta_includes=${{inputs.sync-delta-includes}}` — unquoted assignment (line ~111)
- `git_previous_commit=${{github.event.before}}` — unquoted assignment (line ~222)
- `git_previous_commit=${{github.event.pull_request.base.sha}}` — unquoted assignment (line ~224)
- `cat ${{github.event_path}}` — unquoted path in shell command (line ~127)
- `${{inputs.ftp-options}}` injected verbatim into a heredoc written to ~/.lftprc (line ~175)
- `${{inputs.ssh-options}}` injected into `echo "set sftp:connect-program /usr/bin/ssh -a -x ..."` (lines ~181-183)
- `${{inputs.ftp-mirror-options}}` and `${{inputs.ftp-post-sync-commands}}` injected directly into `lftp -c "..."` command strings (lines ~295, ~302)
- `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — all proxy inputs injected unquoted into ssh command (line ~205)
- `${{inputs.proxy-forwarding-port}}` injected into proxychains config heredoc (line ~165)
- `${{inputs.remote-protocol}}://${{inputs.remote-user}}@${{inputs.remote-host}}:${{inputs.remote-port}}` injected into lftp config (line ~186)
- `${{ github.event.head_commit.message }}` passed as `--arg message` to jq inside the shell function (line ~76) — commit message is attacker-controlled
- `${{inputs.sync-delta-excludes}}` injected into `git diff` command arguments (lines ~237-238)

(b) Unquoted shell variable expansions of untrusted data:
- `input_sync=${{inputs.sync}}` then used in `case`/`if` comparisons without quotes in some places
- `input_sync_delta_includes=${{inputs.sync-delta-includes}}` then used in `for i in ${input_sync_delta_includes//,/ }` — unquoted word-split loop

The most critical injections are `${{inputs.ftp-post-sync-commands}}` and `${{inputs.ftp-mirror-options}}` which are placed directly inside an `lftp -c "..."` command string, allowing arbitrary lftp commands or shell escapes.

Locations:

- `action.yml:76`
- `action.yml:107`
- `action.yml:111`
- `action.yml:127`
- `action.yml:165`
- `action.yml:175`
- `action.yml:181`
- `action.yml:186`
- `action.yml:205`
- `action.yml:222`
- `action.yml:224`
- `action.yml:237`
- `action.yml:295`
- `action.yml:302`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v7` references a mutable version tag (`@v7`) rather than a pinned 40-character commit SHA. This means the action could be silently replaced with a malicious version if the tag is moved, enabling a supply-chain attack.

Locations:

- `action.yml:327`

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

Rewrote action.yml to move all ${{ }} expressions (inputs.remote-protocol, inputs.remote-host, inputs.remote-port, inputs.remote-user, inputs.remote-password, inputs.ssh-private-key, inputs.proxy, inputs.proxy-host, inputs.proxy-port, inputs.proxy-forwarding-port, inputs.proxy-user, inputs.proxy-private-key, inputs.local-path, inputs.remote-path, inputs.sync, inputs.sync-delta-excludes, inputs.sync-delta-includes, inputs.ssh-options, inputs.ftp-options, inputs.ftp-mirror-options, inputs.ftp-post-sync-commands, inputs.webhook, inputs.artifacts, inputs.debug, github.repository, github.workflow, github.job, github.run_id, github.ref, github.event_name, github.actor, github.event.head_commit.message, github.sha, github.event_path, github.event.before, github.event.pull_request.base.sha, github.event.inputs.sync) into an env: block on the Deploy step. The run: block now only references plain environment variables. Also pinned actions/upload-artifact@v7 to full SHA 043fb46d1a93c77aae656e7c1c64a875d1fc6a0a.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 6 script-injection issues in action.yml:
1. Replaced unquoted ${apt_quiet} with apt_quiet_args bash array used as "${apt_quiet_args[@]}" in apt-get calls.
2. Replaced unquoted ${proxy_cmd} in apt-get install with a packages_to_install array that conditionally includes proxychains.
3. Added proxy_cmd_arr array alongside proxy_cmd string; used ${proxy_cmd_arr[@]+"${proxy_cmd_arr[@]}"} pattern for all lftp and curl invocations to safely handle empty/non-empty cases.
4. Fixed INPUT_SSH_OPTIONS embedding in printf: changed from printf '%s\n' "... ${INPUT_SSH_OPTIONS}" to printf '... %s\n' "${INPUT_SSH_OPTIONS}" so the value is a properly quoted printf argument.
5. Fixed unquoted ${input_sync_delta_includes//,/ } for-loop: replaced with IFS=',' read -ra sync_includes_arr <<< "${input_sync_delta_includes}" and for i in "${sync_includes_arr[@]}".
6. Fixed INPUT_FTP_MIRROR_OPTIONS and INPUT_FTP_POST_SYNC_COMMANDS in lftp -c strings: replaced direct string embedding with printf-based command construction using %s format specifiers with all user-controlled values as properly quoted arguments.

### Iteration 3

**Fixes applied:** hardcoded-credentials, script-injection

**Notes:**

Fixed two security issues in action.yml:

1. hardcoded-credentials (line 149): Replaced the literal 'dummypassword' fallback value with `$(openssl rand -hex 16)` to generate a cryptographically random placeholder at runtime instead of using a hardcoded credential string.

2. script-injection (lines 323-330): (a) Added `local_path_unslash_q=$(printf '%q' "${local_path_unslash}")` to shell-quote the caller-controlled local-path value, then used the quoted variable in both sed /e commands to prevent shell metacharacters from being executed via sed's execute flag. (b) Added double-quotes around `$HOME/files_to_upload` and `${local_path_slash}` in the rsync command to prevent word-splitting and glob expansion on the caller-controlled path.

