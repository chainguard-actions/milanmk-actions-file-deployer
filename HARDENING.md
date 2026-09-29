<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.17

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.17** was hardened automatically. 54 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates ${{ }} expressions into shell commands (sub-rule a) and assigns them to unquoted shell variables (sub-rule b), enabling script injection. Critical instances include:

(a) Direct interpolation:
- `--arg message "${{ github.event.head_commit.message }}"` — attacker-controlled commit message injected into jq args
- `curl ... "${{inputs.webhook}}"` — user-controlled URL injected into curl
- `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)` — inputs injected into subshell
- `remote_path_unslash=$(realpath --canonicalize-missing '${{inputs.remote-path}}')` — inputs injected into command
- `input_remote_password="${{inputs.remote-password}}"` — password injected directly
- `echo "${{inputs.ssh-private-key}}" > ${key_ssh}` — private key injected
- `echo "set sftp:connect-program /usr/bin/ssh -a -x ... ${{inputs.ssh-options}}" >> ~/.lftprc` — options injected into config
- `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — multiple inputs injected unquoted into SSH command
- `${{inputs.ftp-post-sync-commands}}` injected directly into lftp -c command string — enables arbitrary lftp command injection
- `${{inputs.ftp-mirror-options}}` injected into lftp -c command string
- `cat ${{github.event_path}}` — github context injected into cat command

(b) Unquoted variable assignments from expressions:
- `input_sync=${{inputs.sync}}` — unquoted assignment
- `input_sync=${{github.event.inputs.sync}}` — unquoted assignment
- `input_sync_delta_includes=${{inputs.sync-delta-includes}}` — unquoted assignment
- `git_previous_commit=${{github.event.before}}` — unquoted assignment
- `git_previous_commit=${{github.event.pull_request.base.sha}}` — unquoted assignment

Locations:

- `action.yml:79`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' uses actions/upload-artifact@v4, which is pinned to a mutable tag (@v4) rather than a full 40-character commit SHA. This is vulnerable to supply-chain attacks if the tag is moved to a different commit. It should be pinned to a specific SHA, e.g., actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4.

Locations:

- `action.yml:261`

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

Rewrote action.yml to fix all findings: (1) Moved all 39 ${{ }} expressions from the 'Deploy' run: block into a step-level env: block, covering all inputs (remote-protocol, remote-host, remote-port, remote-user, remote-password, ssh-private-key, proxy, proxy-host, proxy-port, proxy-forwarding-port, proxy-user, proxy-private-key, local-path, remote-path, sync, sync-delta-excludes, sync-delta-includes, ssh-options, ftp-options, ftp-mirror-options, ftp-post-sync-commands, webhook, artifacts, debug) and all github context values (repository, workflow, job, run_id, ref, event_name, actor, event.head_commit.message, sha, event.before, event.pull_request.base.sha, event.inputs.sync, event_path, toJSON(env), toJSON(inputs)). All shell references now use $VAR_NAME syntax. (2) Pinned actions/upload-artifact@v4 to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with # v4 comment.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all four script-injection issues in action.yml:

1. $INPUT_SSH_OPTIONS (lines 196/198): Tokenized with xargs into ssh_opts array using guard+xargs+read-loop pattern. Each element printed separately with `printf ' %s'` to ~/.lftprc, preventing shell metacharacter injection.

2. $INPUT_SYNC_DELTA_EXCLUDES (lines 254/255): Tokenized with xargs into sync_excludes array. Expanded as "${sync_excludes[@]}" in git diff and git diff-tree commands to preserve argument boundaries.

3. ${ftp_mirror_opts}/${ftp_post_cmds} (lines 288/291/293/300/303): Both tokenized with xargs into arrays (ftp_mirror_opts_arr, ftp_post_cmds_arr). lftp commands now written to a mktemp file using printf statements, and lftp invoked with -f flag instead of -c with a double-quoted string, eliminating shell expansion of user-controlled values.

4. ${proxy_cmd} (multiple locations): Changed from string variable to bash array (proxy_cmd=() or proxy_cmd=(proxychains)). All usages updated to "${proxy_cmd[@]}" which correctly expands to zero words when empty.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script-injection vulnerabilities in action.yml:
1. proxychains config (line ~218): Changed from unquoted $INPUT_PROXY_FORWARDING_PORT embedded in double-quoted string to printf 'socks5 127.0.0.1 %s\n' "$INPUT_PROXY_FORWARDING_PORT" with proper %s format specifier.
2. git commands (lines ~280-282): Added quotes around "${git_previous_commit}" and "${local_path_unslash}" in git cat-file, git diff, and git diff-tree commands.
3. for loop (line ~285): Replaced unquoted word-splitting `for i in ${input_sync_delta_includes//,/ }` with safe `IFS=',' read -ra sync_delta_includes_arr <<< "${input_sync_delta_includes}"` and proper array iteration.
4. sed #e injection (lines ~290-291): Replaced the critical `sed --in-place --regexp-extended "s#(.*)#realpath --canonicalize-missing --relative-to=$local_path_unslash \1#e"` (which executed shell commands with unquoted user input) with a safe while-loop that calls realpath directly with properly quoted arguments.
5. rsync command (line ~296): Added quotes around "$HOME/files_to_upload" and "${local_path_slash}".

