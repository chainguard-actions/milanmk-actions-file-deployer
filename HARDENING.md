<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 54 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ ... }} expressions into shell commands (sub-rule a), allowing script injection. Attacker-controlled values include: github.event.head_commit.message, github.event_name, github.actor, github.event.before, github.event.pull_request.base.sha, github.event.inputs.sync, inputs.webhook, inputs.local-path, inputs.remote-path, inputs.remote-password, inputs.proxy, inputs.sync, inputs.sync-delta-includes, inputs.remote-protocol, inputs.ssh-private-key, inputs.proxy-private-key, inputs.proxy-forwarding-port, inputs.remote-host, inputs.remote-user, inputs.ssh-options, inputs.proxy-user, inputs.proxy-host, inputs.proxy-port, inputs.ftp-options, inputs.ftp-mirror-options, inputs.ftp-post-sync-commands, inputs.sync-delta-excludes, inputs.artifacts, and more. Additionally (sub-rule b), two unquoted shell variable expansions of untrusted data: `input_sync=${{inputs.sync}}` (unquoted, used in comparisons and passed to git commands) and `input_sync_delta_includes=${{inputs.sync-delta-includes}}` (unquoted, iterated in a for loop). Any of these allow an attacker to inject arbitrary shell commands.

Locations:

- `action.yml:68`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v7`, which uses a mutable version tag instead of a pinned 40-character commit SHA. This is vulnerable to supply-chain attacks if the tag is moved. It should be pinned to a full SHA, e.g. `actions/upload-artifact@<40-char-sha> # v7`.

Locations:

- `action.yml:207`

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

1. Moved all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block into a comprehensive env: block on the Deploy step. The run: block now uses only $VAR_NAME environment variable references (e.g., $INPUT_REMOTE_PROTOCOL, $GITHUB_EVENT_NAME, etc.). This fixes all 50+ static-inline-injection and script-injection findings. Also used xargs-based tokenization for the sync-delta-excludes list input. 2. Pinned actions/upload-artifact@v7 to its full commit SHA 043fb46d1a93c77aae656e7c1c64a875d1fc6a0a with a # v7 comment.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 7 script injection issues in action.yml:
1. apt_quiet/proxy_cmd in apt-get: Replaced unquoted ${apt_quiet} with apt_quiet_args array and ${proxy_cmd} with proxy_pkg array.
2. git_previous_commit in git cat-file: Added double-quotes.
3. local_path_unslash in git diff/diff-tree: Added double-quotes.
4. input_sync_delta_includes in for loop: Replaced unquoted word-splitting with safe while/read loop using process substitution.
5. sed 'e' flag with unquoted $local_path_unslash: Replaced dangerous sed 'e' flag execution with a safe while/read/realpath loop.
6. local_path_slash in rsync: Added double-quotes.
7. proxy_cmd/ftp_mirror_opts/ftp_post_sync/paths in lftp commands: Replaced unquoted ${proxy_cmd} with proxy_exec array (defined early), added lftp-level quoting for paths inside lftp -c strings.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed 6 script injection vulnerabilities in action.yml:

1. $INPUT_SSH_OPTIONS (with SSH private key branch): Changed printf '%s\n' "...string...$INPUT_SSH_OPTIONS" to printf 'set sftp:connect-program /usr/bin/ssh -a -x -i ~/ssh_private_key %s\n' "$INPUT_SSH_OPTIONS" — variable is now a printf argument, not expanded in the format string.

2. $INPUT_SSH_OPTIONS (without SSH private key branch): Same fix applied to the else branch.

3. $INPUT_REMOTE_PROTOCOL/$INPUT_REMOTE_USER/$INPUT_REMOTE_HOST/$INPUT_REMOTE_PORT: Changed printf '%s\n' "open $INPUT_REMOTE_PROTOCOL://..." to printf 'open %s://%s@%s:%s\n' "$INPUT_REMOTE_PROTOCOL" "$INPUT_REMOTE_USER" "$INPUT_REMOTE_HOST" "$INPUT_REMOTE_PORT" — all four variables are now printf arguments.

4. $INPUT_PROXY_FORWARDING_PORT in proxychains config: Changed printf '%s\n' "...socks5 127.0.0.1 $INPUT_PROXY_FORWARDING_PORT" to printf '...socks5 127.0.0.1 %s\n' "$INPUT_PROXY_FORWARDING_PORT" — port is now a printf argument.

5-6. ${ftp_mirror_opts} and ${ftp_post_sync} in lftp -c command strings (both full and delta sync branches): Replaced direct embedding in double-quoted lftp command strings with printf-based construction using %s placeholders. The lftp command is built into lftp_cmd variable via printf, then passed as "${lftp_cmd}" to lftp -c. This prevents shell command substitution from executing attacker-controlled content.

### Iteration 1

**Fixes applied:** hardcoded-credentials

**Notes:**

Replaced the hardcoded literal 'dummypassword' fallback value in action.yml (line 163) with a runtime-generated random hex string using `$(openssl rand -hex 16)`. This value is used as a placeholder in the ~/.netrc file when no remote password is provided (e.g., when using SSH key authentication). The fix eliminates the recognizable hardcoded credential pattern while preserving the functional behavior of the action.

