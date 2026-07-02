<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.17

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **milanmk--actions-file-deployer/1.17** was hardened automatically. 54 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ }}` GitHub Actions expressions into shell command strings (sub-rule a), allowing script injection. Attacker-controllable inputs are interpolated without quoting or sanitization, enabling arbitrary command execution. Key violations include:
- `input_sync=${{inputs.sync}}` — unquoted, unquoted assignment allows word-splitting and glob expansion
- `input_sync_delta_includes=${{inputs.sync-delta-includes}}` — unquoted assignment
- `${{inputs.ftp-options}}` written directly into ~/.lftprc config
- `${{inputs.ftp-mirror-options}}` injected into `lftp -c` command string
- `${{inputs.ftp-post-sync-commands}}` injected into `lftp -c` command string (arbitrary lftp commands)
- `${{inputs.ssh-options}}` injected into ssh command line
- `ssh -A -D ${{inputs.proxy-forwarding-port}} ... -p ${{inputs.proxy-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — all injected unquoted into ssh invocation
- `git_previous_commit=${{github.event.before}}` and `${{github.event.pull_request.base.sha}}` — unquoted assignments
- `git rev-parse ${{github.sha}}^` — injected into git command
- `${{inputs.sync-delta-excludes}}` injected into git diff command
- `${{inputs.local-path}}` injected into echo/sed pipeline
- `${{inputs.remote-path}}` injected into realpath command
- `${{inputs.remote-password}}` directly interpolated into shell variable assignment
- `${{inputs.webhook}}` injected as curl URL argument
- `${{inputs.ssh-private-key}}` and `${{inputs.proxy-private-key}}` injected into echo commands
- `cat ${{github.event_path}}` — injected into cat command
- `${{github.event.inputs.sync}}` — injected unquoted
Any of these allow a malicious caller to inject shell metacharacters and execute arbitrary commands on the runner.

Locations:

- `action.yml:68`
- `action.yml:75`
- `action.yml:80`
- `action.yml:84`
- `action.yml:87`
- `action.yml:91`
- `action.yml:100`
- `action.yml:103`
- `action.yml:130`
- `action.yml:155`
- `action.yml:163`
- `action.yml:175`
- `action.yml:183`
- `action.yml:191`
- `action.yml:196`
- `action.yml:210`
- `action.yml:215`
- `action.yml:220`
- `action.yml:232`
- `action.yml:246`
- `action.yml:260`
- `action.yml:263`
- `action.yml:271`
- `action.yml:289`
- `action.yml:295`
- `action.yml:300`
- `action.yml:305`
- `action.yml:340`
- `action.yml:345`
- `action.yml:360`
- `action.yml:375`
- `action.yml:380`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references a mutable tag (`@v4`) instead of a pinned 40-character commit SHA. This means the action could be silently updated to a malicious version without any change to this file, creating a supply-chain attack vector.

Locations:

- `action.yml:393`

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

Rewrote action.yml to move all ${{ }} GitHub Actions expressions from the run: shell block into a dedicated env: block on the Deploy step. Created 37 environment variables covering all inputs (remote-protocol, remote-host, remote-port, remote-user, remote-password, ssh-private-key, proxy, proxy-host, proxy-port, proxy-forwarding-port, proxy-user, proxy-private-key, local-path, remote-path, sync, sync-delta-excludes, sync-delta-includes, ssh-options, ftp-options, ftp-mirror-options, ftp-post-sync-commands, webhook, artifacts, debug) and all github context values (repository, workflow, job, run_id, ref, event_name, actor, event.head_commit.message, sha, event.before, event.pull_request.base.sha, event_path, event.inputs.sync). The run: block now references only plain $VAR_NAME shell variables. Also pinned actions/upload-artifact@v4 to its full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script injection sub-issues in action.yml:

1. INPUT_PROXY_FORWARDING_PORT: Sanitized with bash parameter expansion ${INPUT_PROXY_FORWARDING_PORT//[^0-9]/} to allow only digits before writing to proxychains config.

2. INPUT_SSH_OPTIONS: Changed printf from embedding the variable in the format string to passing it as a properly-quoted printf argument: `printf 'set sftp:connect-program /usr/bin/ssh -a -x %s\n' "$INPUT_SSH_OPTIONS"`.

3. INPUT_SYNC_DELTA_EXCLUDES: Replaced unquoted ${INPUT_SYNC_DELTA_EXCLUDES} in git diff/diff-tree with a bash array (sync_delta_excludes_args) built by reading space-separated values, then expanded as "${sync_delta_excludes_args[@]}".

4. INPUT_FTP_MIRROR_OPTIONS and INPUT_FTP_POST_SYNC_COMMANDS: Refactored lftp invocation from `lftp -c "...${VAR}..."` (where bash double-quoting still allows $() command substitution) to writing lftp commands to a mktemp file using printf with properly-quoted arguments, then running `lftp -f "${lftp_script}"`. This eliminates both bash-level injection and lftp command injection risks.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed two script injection vulnerabilities in action.yml:
1. Replaced unquoted `for i in ${input_sync_delta_includes//,/ }` with `IFS=',' read -ra _sync_includes <<< "${input_sync_delta_includes}"` and `for i in "${_sync_includes[@]}"` to safely split the comma-separated user input without allowing shell metacharacter injection.
2. Replaced two `sed --in-place --regexp-extended "s#(.*)#realpath --canonicalize-missing --relative-to=$local_path_unslash \1#e"` commands (which used sed's dangerous `#e` flag to execute shell commands with unquoted user-controlled `$local_path_unslash`) with safe `while IFS= read -r _line` loops that call `realpath` directly with properly quoted arguments, writing to temp files and atomically replacing the originals.

### Iteration 4

**Fixes applied:** hardcoded-credentials, script-injection

**Notes:**

1. hardcoded-credentials (line 152): Replaced the hardcoded fallback value 'dummypassword' with an empty string in the `input_remote_password` assignment. The dummy password was unnecessary since lftp supports key-based authentication and empty passwords. 2. script-injection (line 196): Converted `apt_quiet` string variable to a bash array `apt_quiet_args` (containing '--quiet' '--quiet' or empty), converted `proxy_cmd` string variable to a bash array, and built a `pkg_list` array for packages to install. All usages now use proper `"${array[@]}"` expansion, eliminating unquoted variable expansion of user-controlled data. Also updated the two other active usages of `${proxy_cmd}` (in the curl and lftp commands) to use `"${proxy_cmd[@]}"` array expansion for consistency and safety.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed all 6 script-injection issues in action.yml:
1. Quoted `${git_previous_commit}` in `git cat-file -t` call (line 248) to prevent word splitting.
2. Quoted `${local_path_slash}` and `$HOME/files_to_upload` in rsync command (line 277) to prevent word splitting on paths with spaces.
3. Sanitized INPUT_FTP_OPTIONS by stripping newlines/carriage returns before writing to ~/.lftprc (line 196), preventing lftp config injection via embedded newlines.
4. Sanitized INPUT_SSH_OPTIONS by stripping newlines/carriage returns before writing to ~/.lftprc (line 199), preventing lftp config injection.
5. Sanitized INPUT_FTP_MIRROR_OPTIONS by stripping newlines/carriage returns before writing to lftp script (line 295), preventing lftp command injection via embedded newlines.
6. Sanitized INPUT_FTP_POST_SYNC_COMMANDS by stripping carriage returns (preserving intentional newlines for multi-command support) before writing to lftp script (line 302). All ${{ }} expressions were already in the env: block.

