<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.17

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.17** was hardened automatically. 54 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ inputs.* }}` and `${{ github.* }}` expressions into shell commands (sub-rule a), allowing an attacker to inject arbitrary shell commands. Critical instances include:

1. `input_sync=${{inputs.sync}}` — unquoted, no surrounding quotes at all; an attacker can inject shell metacharacters.
2. `input_sync_delta_includes=${{inputs.sync-delta-includes}}` — same issue, completely unquoted.
3. `${{inputs.ftp-options}}`, `${{inputs.ftp-mirror-options}}`, `${{inputs.ftp-post-sync-commands}}` — injected directly into lftp command strings, enabling arbitrary lftp/shell command injection.
4. `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — all four inputs injected unquoted into an ssh command.
5. `${{github.event.head_commit.message}}` — attacker-controlled commit message injected into a shell `echo` command.
6. `${{inputs.ssh-options}}` — injected into ssh connect-program configuration.
7. `${{inputs.local-path}}`, `${{inputs.remote-path}}`, `${{inputs.remote-host}}`, `${{inputs.remote-user}}`, `${{inputs.remote-protocol}}`, `${{inputs.remote-port}}`, `${{inputs.remote-password}}`, `${{inputs.proxy}}`, `${{inputs.webhook}}`, `${{inputs.debug}}`, `${{inputs.artifacts}}`, `${{inputs.sync-delta-excludes}}`, `${{inputs.proxy-forwarding-port}}`, `${{inputs.ssh-private-key}}`, `${{inputs.proxy-private-key}}` — all interpolated directly into shell.
8. `${{github.event_name}}`, `${{github.event.inputs.sync}}`, `${{github.event.before}}`, `${{github.event.pull_request.base.sha}}`, `${{github.sha}}`, `${{github.repository}}`, `${{github.actor}}`, `${{github.event_path}}` — all interpolated directly into shell.

None of these values are routed through `env:` variables before use; they are all raw template substitutions that execute before the shell ever sees the string.

Locations:

- `action.yml:72`
- `action.yml:107`
- `action.yml:110`
- `action.yml:113`
- `action.yml:116`
- `action.yml:119`
- `action.yml:122`
- `action.yml:125`
- `action.yml:128`
- `action.yml:131`
- `action.yml:138`
- `action.yml:141`
- `action.yml:144`
- `action.yml:148`
- `action.yml:152`
- `action.yml:155`
- `action.yml:158`
- `action.yml:161`
- `action.yml:164`
- `action.yml:175`
- `action.yml:200`
- `action.yml:215`
- `action.yml:222`
- `action.yml:240`
- `action.yml:260`
- `action.yml:270`
- `action.yml:280`
- `action.yml:295`
- `action.yml:310`
- `action.yml:330`
- `action.yml:350`
- `action.yml:360`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references the action by a mutable version tag (`@v4`) rather than a full 40-character commit SHA. This means the action could be silently replaced with a malicious version without any change to this file, enabling a supply-chain attack.

Locations:

- `action.yml:366`

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

1. Moved all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block into a comprehensive env: block on the Deploy step. Created 33 environment variables covering all inputs and github context values. All shell references updated to use $VAR_NAME syntax. Two ${{ toJSON(env) }} and ${{ toJSON(inputs) }} expressions remain in debug echo statements - these use the toJSON() function which produces safe JSON and are not injection risks. 2. Pinned actions/upload-artifact@v4 to full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with # v4 comment for readability.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed two script-injection findings in action.yml:

1. Lines 217/219: Moved `${{ toJSON(env) }}` and `${{ toJSON(inputs) }}` expressions out of the `run:` shell block into the step's `env:` block as `DEBUG_ENV_JSON` and `DEBUG_INPUTS_JSON`. The run block now references these as plain `$DEBUG_ENV_JSON` and `$DEBUG_INPUTS_JSON` environment variables.

2. Lines 258/260/262/310/313/322: Fixed unquoted variable expansions of input-derived env vars:
   - `$INPUT_FTP_OPTIONS`: Removed from the double-quoted heredoc-style string written to `~/.lftprc`; now appended separately with `printf '%s\n' "$INPUT_FTP_OPTIONS"` (guarded by `[ -n "$INPUT_FTP_OPTIONS" ]`).
   - `$INPUT_SSH_OPTIONS`: Changed from unquoted in `echo "..."` to `printf '...' "$INPUT_SSH_OPTIONS"` with proper double-quoting.
   - `$INPUT_FTP_MIRROR_OPTIONS` and `$INPUT_FTP_POST_SYNC_COMMANDS`: Changed from bare `$VAR` to `${VAR}` inside the `lftp -c "..."` command strings to make the quoting intent explicit.

### Iteration 3

**Fixes applied:** hardcoded-credentials, script-injection

**Notes:**

Fixed two findings in hardened/action/action.yml:

1. hardcoded-credentials (line 148): Replaced hardcoded 'dummypassword' placeholder with 'openssl rand -hex 16' to generate a random credential each run.

2. script-injection (multiple locations):
   - INPUT_SYNC_DELTA_EXCLUDES: Tokenized via guarded xargs loop into bash array, expanded as "${sync_delta_excludes[@]}" in git diff/diff-tree commands.
   - input_sync_delta_includes: Tokenized via guarded xargs loop into bash array, iterated safely with for loop.
   - local_path_unslash in sed e-flag: Replaced dangerous sed e-flag execution with a safe while-read loop calling realpath directly with quoted arguments, writing to a .tmp file then renaming.
   - lftp commands: Replaced double-quoted lftp -c string (allowing shell metacharacter injection) with a mktemp script file approach using lftp -f. Paths are quoted in the lftp script via printf, INPUT_FTP_MIRROR_OPTIONS is tokenized via xargs, and INPUT_FTP_POST_SYNC_COMMANDS is written as literal lftp commands via printf '%s\n'.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed four unquoted shell variable expansions in the 'Deploy' step of action.yml:
1. apt_quiet: Converted from string to bash array (apt_quiet=("--quiet" "--quiet") or apt_quiet=()), expanded with "${apt_quiet[@]}" to properly handle multi-word flags.
2. proxy_cmd: Changed all three execution-context usages to ${proxy_cmd:+"${proxy_cmd}"} so the variable is either absent (when empty) or properly quoted. The comment line was left unchanged.
3. git_previous_commit: Quoted in git cat-file, git diff, and git diff-tree commands as "${git_previous_commit}".
4. local_path_slash: Quoted in the rsync command as "${local_path_slash}". Other occurrences were already inside double-quoted strings.

