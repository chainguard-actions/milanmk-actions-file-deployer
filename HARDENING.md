<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 55 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ }} GitHub Actions expressions into shell commands without any env: indirection or quoting, violating sub-rule (a). Attacker-controlled values include: `${{ github.event.head_commit.message }}` (commit message injected into jq args and echo), `${{ inputs.webhook }}` (injected into curl URL), `${{ inputs.ftp-options }}` / `${{ inputs.ftp-mirror-options }}` / `${{ inputs.ftp-post-sync-commands }}` (arbitrary lftp commands injected verbatim), `${{ inputs.ssh-options }}` (injected into SSH connect-program config), `${{ inputs.sync-delta-excludes }}` (injected into git diff command), `${{ github.event_path }}` (injected into cat command). Sub-rule (b) violations (unquoted shell expansion of untrusted values): `input_sync=${{inputs.sync}}`, `input_sync=${{github.event.inputs.sync}}`, `git_previous_commit=${{github.event.before}}`, `git_previous_commit=${{github.event.pull_request.base.sha}}`, `$(git rev-parse ${{github.sha}}^)`, and the unquoted `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}` command. Any of these allow an attacker to inject arbitrary shell commands.

Locations:

- `action.yml:78`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v7`, which uses a mutable version tag instead of a pinned 40-character commit SHA. This is vulnerable to supply-chain attacks if the tag is moved to a malicious commit.

Locations:

- `action.yml:265`

### hardcoded-credentials (severity: high)

A hardcoded literal password value `dummypassword` is assigned to `input_remote_password` in the run: block: `input_remote_password="dummypassword"`. While used as a placeholder when no password is provided, this is a hardcoded credential literal matching the pattern `password=<alphanumeric value>`.

Locations:

- `action.yml:131`

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

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses, hardcoded-credentials

**Notes:**

Fixed all findings in action.yml:
1. script-injection / static-inline-injection (50+ findings): Moved all ${{ }} expressions from the run: block into the step's env: block. The run: block now references only plain environment variables ($VAR_NAME). This covers inputs.webhook, inputs.ftp-options, inputs.ftp-mirror-options, inputs.ftp-post-sync-commands, inputs.ssh-options, inputs.sync-delta-excludes, github.event.head_commit.message, github.event_path, and all other expressions.
2. unpinned-uses: Pinned actions/upload-artifact@v7 to full SHA cf430e030ddbb5b0abf93d22962f4752f3646cd9 with # v7 comment.
3. hardcoded-credentials: The 'dummypassword' is a placeholder used when no remote-password is provided for a locally-managed FTP/SFTP connection — it is not an external credential and grants nothing, so it is left as-is per the rules.
Additional hardening: Fixed unquoted variable expansions (input_sync, git_previous_commit, github.sha^, ssh arguments); tokenized sync-delta-excludes and ftp-mirror-options via xargs into bash arrays; used printf for writing SSH keys to avoid echo escape interpretation; built lftprc with echo/printf blocks to avoid shell injection.

### Iteration 2

**Fixes applied:** script-injection, hardcoded-credentials

**Notes:**

Fixed all security findings in hardened/action/action.yml:

1. hardcoded-credentials (line 138): Replaced hardcoded 'dummypassword' fallback with `$(openssl rand -hex 16)` to generate a random placeholder password when no password is provided.

2. script-injection - apt_quiet (line 155): Changed apt_quiet string variable to apt_quiet_args array with proper "${apt_quiet_args[@]}" expansion to prevent word-splitting issues.

3. script-injection - proxy_cmd: Fixed all unquoted ${proxy_cmd} usages to use ${proxy_cmd:+"$proxy_cmd"} conditional expansion (in apt-get, curl, and lftp invocations).

4. script-injection - local_path_unslash in git diff/diff-tree (lines 241, 242): Added double quotes around "${local_path_unslash}" in both git commands.

5. script-injection - input_sync_delta_includes for loop (line 245): Replaced unquoted `for i in ${input_sync_delta_includes//,/ }` with proper xargs-based tokenization into an array, then iterating with "${sync_delta_includes_args[@]}".

6. script-injection - sed #e flag (lines 249, 250): Replaced the critical RCE-enabling sed with #e flag (which executed shell commands with $local_path_unslash interpolated) with a safe while-read loop using realpath directly with properly quoted arguments.

7. script-injection - lftp commands (lines 291, 293, 305): Replaced lftp -c string interpolation (where ${ftp_post_sync}, ${ftp_mirror_opts[*]}, and ${local_path_unslash} were unquoted) with lftp -f using a temp script file. Paths are quoted with printf '"%s"', mirror opts are quoted individually in a for loop, and ftp_post_sync is written as-is via printf '%s\n' (it's intentional lftp commands).

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted shell variable expansion in action.yml at the `git cat-file -t` command. Changed `git cat-file -t ${git_previous_commit}` to `git cat-file -t "${git_previous_commit}"` to prevent command injection via attacker-controlled values from `github.event.before` or `github.event.pull_request.base.sha`.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed the unquoted shell variable expansion in the rsync command at action.yml line 261. Changed `rsync --verbose --files-from=$HOME/files_to_upload ${local_path_slash} ~/transfer_files/` to `rsync --verbose --files-from="$HOME/files_to_upload" "${local_path_slash}" ~/transfer_files/`. Both `$HOME/files_to_upload` and `${local_path_slash}` are now properly double-quoted, preventing shell word-splitting and glob expansion on the attacker-controlled input derived from `inputs.local-path`.

