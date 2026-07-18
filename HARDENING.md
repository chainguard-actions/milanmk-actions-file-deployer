<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 54 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ }}` GitHub Actions expressions into shell commands without routing them through env vars or quoting them safely. This is a sub-rule (a) violation. Attacker-controllable values are especially dangerous: `${{ github.event.head_commit.message }}` (commit message can contain shell metacharacters), `${{ github.event.inputs.sync }}` (workflow_dispatch input), `${{ github.event.before }}` and `${{ github.event.pull_request.base.sha }}` (PR/push event data), and all `${{ inputs.* }}` values (e.g. `inputs.remote-host`, `inputs.remote-user`, `inputs.ssh-options`, `inputs.proxy-user`, `inputs.proxy-host`, `inputs.ftp-options`, `inputs.ftp-mirror-options`, `inputs.ftp-post-sync-commands`, `inputs.webhook`). These are interpolated directly into shell strings before the shell ever parses them, enabling command injection. Notable examples include: `input_sync=${{inputs.sync}}` (unquoted), `input_sync=${{github.event.inputs.sync}}` (unquoted), `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}` (unquoted SSH args), `${{inputs.ftp-post-sync-commands}}` injected directly into an lftp -c string, and `${{inputs.ftp-options}}` written into ~/.lftprc.

Locations:

- `action.yml:68`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v7` references a mutable version tag (`@v7`) instead of a pinned full 40-character commit SHA. This is vulnerable to supply-chain attacks if the tag is moved or the upstream repository is compromised.

Locations:

- `action.yml:222`

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

1. Moved all ${{ }} GitHub Actions expressions (inputs.*, github.event.*, github.sha, github.actor, github.workflow, github.job, github.run_id, github.ref, github.event_name, github.repository, github.event_path, github.event.head_commit.message, github.event.inputs.sync, github.event.before, github.event.pull_request.base.sha) out of the run: block and into a comprehensive env: block on the Deploy step. The run: block now references only plain environment variables ($VAR_NAME) preventing shell injection. 2. Pinned actions/upload-artifact@v7 to the full commit SHA 043fb46d1a93c77aae656e7c1c64a875d1fc6a0a with a # v7 comment for readability.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script injection vulnerabilities in hardened/action/action.yml:

1. $INPUT_SSH_OPTIONS (lines 222, 224): Changed printf format from embedding variable inside double-quoted string to using '%s' format specifier with double-quoted "$INPUT_SSH_OPTIONS" argument. This prevents word-splitting and glob expansion.

2. $INPUT_REMOTE_PROTOCOL, $INPUT_REMOTE_USER, $INPUT_REMOTE_HOST, $INPUT_REMOTE_PORT (line 226): Changed printf to use separate '%s' format specifiers for each variable, each passed as a double-quoted argument.

3. $INPUT_SYNC_DELTA_EXCLUDES (lines 278, 279): Changed from unquoted bare expansion to using 'read -r -a sync_delta_excludes_arr <<< "$INPUT_SYNC_DELTA_EXCLUDES"' and then '"${sync_delta_excludes_arr[@]}"' to safely handle multiple excludes as an array.

4. $INPUT_FTP_MIRROR_OPTIONS and $INPUT_FTP_POST_SYNC_COMMANDS (lines 318, 320, 327): Changed from direct interpolation inside double-quoted lftp -c strings to building the command string via printf with '%s' format specifiers and double-quoted arguments, then passing the result as "$lftp_cmd" to lftp -c.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all 7 script-injection violations in action.yml:
1. Converted apt_quiet string variable to bash array (apt_quiet_args) to safely handle empty/multi-word values with '${apt_quiet_args[@]}'
2. Converted proxy_cmd apt-get argument to bash array (proxy_install_args) with '${proxy_install_args[@]}'
3. Quoted ${git_previous_commit} in 'git cat-file -t' command
4. Quoted ${git_previous_commit} and ${local_path_unslash} in 'git diff' command
5. Quoted ${git_previous_commit} and ${local_path_unslash} in 'git diff-tree' command
6. Replaced unquoted word-splitting 'for i in ${input_sync_delta_includes//,/ }' with safe 'IFS=, read -ra' array approach
7. Replaced dangerous 'sed --regexp-extended s#...#...#e' (which executes shell commands) with safe 'while IFS= read -r _line; do realpath ...; done' loop that properly quotes $local_path_unslash
8. Quoted ${local_path_slash} and $HOME/files_to_upload in rsync command

### Iteration 4

**Fixes applied:** hardcoded-credentials

**Notes:**

Replaced the hardcoded literal 'dummypassword' fallback value (assigned to input_remote_password when INPUT_REMOTE_PASSWORD is empty) with '$(openssl rand -hex 16)'. This generates a cryptographically random 32-character hex string at runtime, eliminating the static hardcoded credential while preserving the functional requirement of providing a non-empty placeholder for the .netrc file used by lftp.

### Iteration 5

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script-injection sub-issues in hardened/action/action.yml:
1. netrc write: replaced echo with printf using %s format specifiers for $INPUT_REMOTE_HOST, $INPUT_REMOTE_USER, and password.
2. proxychains config: replaced embedded $INPUT_PROXY_FORWARDING_PORT in printf string with a %s format argument.
3. SSH options: sanitized $INPUT_SSH_OPTIONS with tr -d '\n\r' before writing to lftp config to prevent newline-based lftp directive injection.
4. SSH proxy command: replaced concatenated "$INPUT_PROXY_USER@$INPUT_PROXY_HOST" with separate -l "$INPUT_PROXY_USER" "$INPUT_PROXY_HOST" arguments to prevent SSH option injection.
5. FTP commands: sanitized $INPUT_FTP_MIRROR_OPTIONS and $INPUT_FTP_POST_SYNC_COMMANDS with tr -d '\n\r' before use in lftp command construction.

