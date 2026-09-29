<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 54 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block directly interpolates dozens of ${{ }} GitHub Actions expressions into shell commands (sub-rule a), including attacker-controlled values such as: `${{ github.event.head_commit.message }}` (commit message, fully attacker-controlled on PRs), `${{ github.event.inputs.sync }}` (workflow_dispatch input), `${{ github.event.before }}`, `${{ github.event.pull_request.base.sha }}`, `${{ inputs.remote-host }}`, `${{ inputs.remote-user }}`, `${{ inputs.remote-path }}`, `${{ inputs.ssh-options }}`, `${{ inputs.ftp-options }}`, `${{ inputs.ftp-mirror-options }}`, `${{ inputs.ftp-post-sync-commands }}`, `${{ inputs.proxy-user }}`, `${{ inputs.proxy-host }}`, `${{ inputs.sync-delta-excludes }}`, and more. All are interpolated before the shell parses the script, enabling arbitrary command injection. Sub-rule (b) violations include: `input_sync=${{inputs.sync}}` used unquoted in subsequent shell commands; `input_sync_delta_includes=${{inputs.sync-delta-includes}}` used unquoted in a for-loop (`for i in ${input_sync_delta_includes//,/ }`), allowing word-splitting and glob expansion; `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` injects inputs directly into an SSH command; and `${{inputs.ftp-post-sync-commands}}` is injected directly into an lftp -c string, allowing arbitrary lftp commands.

Locations:

- `action.yml:97`
- `action.yml:113`
- `action.yml:122`
- `action.yml:125`
- `action.yml:128`
- `action.yml:131`
- `action.yml:134`
- `action.yml:137`
- `action.yml:140`
- `action.yml:143`
- `action.yml:155`
- `action.yml:158`
- `action.yml:163`
- `action.yml:167`
- `action.yml:170`
- `action.yml:173`
- `action.yml:176`
- `action.yml:200`
- `action.yml:207`
- `action.yml:210`
- `action.yml:213`
- `action.yml:232`
- `action.yml:246`
- `action.yml:249`
- `action.yml:252`
- `action.yml:255`
- `action.yml:258`
- `action.yml:261`
- `action.yml:264`
- `action.yml:267`
- `action.yml:270`
- `action.yml:273`
- `action.yml:276`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v7`, which uses a mutable version tag (`v7`) instead of a pinned 40-character commit SHA. This means the referenced action could be silently replaced with a malicious version without any change to this file, creating a supply-chain risk.

Locations:

- `action.yml:320`

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

1. All ${{ }} expressions moved from the run: block to a comprehensive env: block. Every input (remote-protocol, remote-host, remote-port, remote-user, remote-password, ssh-private-key, proxy, proxy-host, proxy-port, proxy-forwarding-port, proxy-user, proxy-private-key, local-path, remote-path, sync, sync-delta-excludes, sync-delta-includes, ssh-options, ftp-options, ftp-mirror-options, ftp-post-sync-commands, webhook, artifacts, debug) and every github context value (repository, workflow, job, run_id, ref, event_name, actor, sha, event_path, event.head_commit.message, event.before, event.pull_request.base.sha, event.inputs.sync, toJSON(env), toJSON(inputs)) is now mapped to an env var. The shell script uses only $VAR_NAME references. 2. sync-delta-excludes is tokenized via xargs into a bash array for safe argument passing. 3. ftp-mirror-options is tokenized via xargs into a bash array. 4. The lftprc generation was refactored to use a { ... } > file block to safely include ftp-options. 5. SSH proxy command arguments are properly double-quoted. 6. actions/upload-artifact@v7 pinned to full SHA @043fb46d1a93c77aae656e7c1c64a875d1fc6a0a # v7.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script injection findings in action.yml:

1. Lines 196/198 ($INPUT_SSH_OPTIONS): Replaced `echo "set sftp:connect-program ... $INPUT_SSH_OPTIONS"` with `printf 'set sftp:connect-program ... %s\n' "$INPUT_SSH_OPTIONS"` to properly quote the variable.

2. Lines 247/254 ($INPUT_FTP_POST_SYNC_COMMANDS): Replaced direct interpolation into lftp -c string with writing commands to a temp file via `printf '%s\n' "$INPUT_FTP_POST_SYNC_COMMANDS" > "$ftp_post_sync_script"` and using lftp's `source` command to include the file.

3. Line 200 ($INPUT_REMOTE_PROTOCOL, $INPUT_REMOTE_USER, $INPUT_REMOTE_HOST, $INPUT_REMOTE_PORT): Replaced `echo "open $INPUT_REMOTE_PROTOCOL://$INPUT_REMOTE_USER@$INPUT_REMOTE_HOST:$INPUT_REMOTE_PORT"` with `printf 'open %s://%s@%s:%s\n' "$INPUT_REMOTE_PROTOCOL" "$INPUT_REMOTE_USER" "$INPUT_REMOTE_HOST" "$INPUT_REMOTE_PORT"`.

4. Line 222 (${input_sync_delta_includes//,/ }): Replaced unquoted for loop with safe `while IFS= read -r -d ',' i; do ... done <<< "${input_sync_delta_includes},"` to prevent word-splitting and glob expansion.

5. Lines 228/229 ($local_path_unslash in sed with #e flag): Added `local_path_escaped=$(printf '%s' "$local_path_unslash" | sed 's/[&#\]/\\&/g; s|#|\\#|g')` to escape special characters before embedding the path in the sed expression that uses the dangerous #e execution flag.

### Iteration 3

**Fixes applied:** hardcoded-credentials, script-injection

**Notes:**

Fixed two security findings in hardened/action/action.yml:

1. hardcoded-credentials (line 130): Removed the 'dummypassword' fallback string. The if-block that assigned 'dummypassword' when INPUT_REMOTE_PASSWORD was empty was eliminated; input_remote_password now simply holds $INPUT_REMOTE_PASSWORD directly.

2. script-injection (lines 165, 200, 295, 342): Fixed four injection points:
   - proxy_cmd converted from a string variable to a bash array (proxy_cmd=() / proxy_cmd=(proxychains)), with all usages updated to "${proxy_cmd[@]}" — this safely handles the empty-array case (no proxy) and the single-element case (proxychains), preventing word-splitting injection
   - $INPUT_PROXY_FORWARDING_PORT in the proxychains config now written via printf '%s' with proper quoting instead of unquoted interpolation in an echo string
   - ${local_path_unslash} in git diff and git diff-tree commands now properly double-quoted as "${local_path_unslash}"
   - ${local_path_unslash} in the lftp mirror command now properly escaped-quoted as \"${local_path_unslash}\" within the lftp -c string
   - All ${proxy_cmd} command prefixes replaced with "${proxy_cmd[@]}" in lftp invocations and curl check

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed three script-injection vulnerabilities in action.yml:

1. Quoted `${git_previous_commit}` in `git cat-file -t` command (was unquoted, allowing shell metacharacter injection from attacker-controlled GitHub event before-SHA or PR base SHA).

2. Replaced dangerous `sed --regexp-extended 's#(.*)#realpath ... --relative-to=${local_path_escaped} \1#e'` pattern (which executes the substitution as a shell command via the `#e` flag) with a safe `while IFS= read -r filepath; do realpath --canonicalize-missing --relative-to="$local_path_unslash" "$filepath"; done` loop. This eliminates the shell execution vector entirely — `$INPUT_LOCAL_PATH` values containing `$(...)`, backticks, or semicolons can no longer be executed as shell commands.

3. Quoted `${local_path_slash}` and `$HOME/files_to_upload` in the `rsync` command to prevent word splitting and glob expansion on attacker-controlled path data.

### Iteration 5

**Fixes applied:** script-injection

**Notes:**

Fixed the script injection vulnerability in the full sync lftp command. Replaced `lftp -c "..."` (which had unquoted `${ftp_mirror_opts[*]}` and `${remote_path_unslash}` expansions) with writing lftp commands to a temporary script file using `printf` format specifiers, then executing with `lftp -f script_file`. This eliminates word-splitting and shell metacharacter injection risks. The `ftp_mirror_opts` array is now expanded with `"${ftp_mirror_opts[@]}"` (properly quoted) and each option is written as a separate quoted lftp argument via printf.

