<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.17

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.17** was hardened automatically. 54 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The single `run:` block in action.yml directly interpolates dozens of `${{ inputs.* }}` and `${{ github.* }}` expressions into shell commands without quoting, violating rule (a). An attacker-controlled calling workflow can supply values containing shell metacharacters (`;`, `|`, `&`, `$(...)`, etc.) to achieve arbitrary command execution. Key dangerous instances include:

- `input_sync=${{inputs.sync}}` — unquoted assignment; shell word-splits the value (line ~100)
- `input_sync_delta_includes=${{inputs.sync-delta-includes}}` — unquoted assignment (line ~104)
- `input_sync=${{github.event.inputs.sync}}` — unquoted assignment from attacker-controlled event input (line ~102)
- `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — multiple unquoted inputs injected directly into an SSH command (line ~196)
- `${{inputs.ftp-options}}` injected verbatim into the lftp config file written via a here-string (line ~168)
- `${{inputs.ssh-options}}` injected verbatim into the lftp sftp:connect-program config (line ~178)
- `${{inputs.ftp-mirror-options}}` and `${{inputs.ftp-post-sync-commands}}` injected directly into lftp `-c` command strings (lines ~248, ~254)
- `git_previous_commit=${{github.event.before}}` and `git_previous_commit=${{github.event.pull_request.base.sha}}` — unquoted assignments from attacker-controlled event data (lines ~228, ~230)
- `realpath --canonicalize-missing '${{inputs.remote-path}}'` — single-quoted but still allows injection of single-quote characters (line ~88)
- `git diff ... ${{inputs.sync-delta-excludes}}` — unquoted, injected into git command (lines ~237–238)

All `${{ ... }}` expressions must be moved to `env:` variables and then double-quoted in the shell script.

Locations:

- `action.yml:75`
- `action.yml:88`
- `action.yml:100`
- `action.yml:102`
- `action.yml:104`
- `action.yml:168`
- `action.yml:178`
- `action.yml:180`
- `action.yml:196`
- `action.yml:228`
- `action.yml:230`
- `action.yml:237`
- `action.yml:238`
- `action.yml:248`
- `action.yml:254`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references a mutable version tag (`v4`) rather than an immutable 40-character commit SHA. If the `actions/upload-artifact` repository is compromised or the tag is moved, malicious code could be injected into this action's execution. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:271`

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

Rewrote hardened/action/action.yml to fix all security findings:

1. **script-injection / static-inline-injection (50+ instances)**: Moved all ${{ inputs.* }} and ${{ github.* }} expressions out of the run: shell block into a comprehensive env: block on the Deploy step. The shell script now references only plain environment variables with proper double-quoting. Key changes include:
   - All inputs (remote-protocol, remote-host, remote-port, remote-user, remote-password, ssh-private-key, proxy, proxy-host, proxy-port, proxy-forwarding-port, proxy-user, proxy-private-key, local-path, remote-path, sync, sync-delta-excludes, sync-delta-includes, ssh-options, ftp-options, ftp-mirror-options, ftp-post-sync-commands, webhook, artifacts, debug) mapped to INPUT_* env vars
   - All github context values (repository, workflow, job, run_id, ref, event_name, actor, sha, event_path, event.before, event.pull_request.base.sha, event.inputs.sync, event.head_commit.message) mapped to GITHUB_*_VAR env vars
   - SSH command now uses quoted "$INPUT_PROXY_USER@$INPUT_PROXY_HOST" and quoted port/forwarding-port args
   - sync-delta-excludes handled via bash array (read -ra) to avoid word-splitting injection
   - lftprc config written via printf instead of here-string to avoid injection
   - realpath now uses double-quoted "$INPUT_REMOTE_PATH" instead of single-quoted with injection risk

2. **unpinned-uses**: Pinned actions/upload-artifact@v4 to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with # v4 comment.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all four script injection vulnerabilities in action.yml:
1. Replaced unquoted `for i in ${input_sync_delta_includes//,/ }` with safe `IFS=',' read -ra _includes` + quoted array iteration to prevent glob expansion and word-splitting.
2. Replaced dangerous `sed #e` execute flag (which ran shell commands with unquoted user-controlled `$local_path_unslash`) with `xargs -d '\n' -I{} realpath --canonicalize-missing --relative-to="$local_path_unslash" {}` which properly quotes the path.
3. Quoted `$HOME/files_to_upload` and `${local_path_slash}` in the rsync command.
4. Replaced unquoted `${mirror_opts}` and `${post_cmds}` embedded in lftp `-c` shell strings with a temp script file approach using `mktemp` + `lftp -f`, writing user-controlled values via `printf '%s'` to prevent shell metacharacter injection.

### Iteration 3

**Fixes applied:** script-injection, hardcoded-credentials

**Notes:**

Two fixes applied to hardened/action/action.yml: (1) Quoted the `${git_previous_commit}` variable in `git cat-file -t "${git_previous_commit}"` to prevent shell metacharacter injection from attacker-controlled GitHub context values (github.event.before and github.event.pull_request.base.sha). (2) Replaced the hardcoded literal `dummypassword` placeholder with `$(openssl rand -hex 16)` to generate a random value at runtime instead of using a static credential string.

