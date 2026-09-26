<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 5 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' step's run: block in action.yml directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions into shell commands (rule a). This allows any caller to inject arbitrary shell commands. Critical examples include: (1) `input_sync=${{inputs.sync}}` — unquoted, direct shell word-splitting injection; (2) `${{inputs.ftp-post-sync-commands}}` injected verbatim into an lftp -c command string; (3) `${{inputs.ssh-options}}` injected into an ssh command; (4) `${{inputs.sync-delta-excludes}}` injected into git diff; (5) `${{inputs.ftp-mirror-options}}` injected into lftp mirror; (6) `${{inputs.remote-path}}` passed to realpath; (7) `${{github.event.head_commit.message}}`, `${{github.actor}}`, `${{github.ref}}` and other github context values interpolated into jq arguments and echo statements. All of these bypass shell quoting and allow command injection by a malicious caller or pull request author.

Locations:

- `action.yml:75`
- `action.yml:76`
- `action.yml:77`
- `action.yml:78`
- `action.yml:79`
- `action.yml:80`
- `action.yml:81`
- `action.yml:82`
- `action.yml:83`
- `action.yml:88`
- `action.yml:97`
- `action.yml:100`
- `action.yml:102`
- `action.yml:107`
- `action.yml:112`
- `action.yml:113`
- `action.yml:117`
- `action.yml:130`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' uses `actions/upload-artifact@v4`, which is pinned to a mutable version tag (`v4`) rather than an immutable 40-character commit SHA. This means the action could be silently replaced with a malicious version without any change to this file.

Locations:

- `action.yml:207`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:117`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:120`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.local-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:131`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-path}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:134`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:137`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-password}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:138`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:142`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:149`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:156`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:156`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:157`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:170`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:188`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:202`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:206`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:206`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:207`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:210`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:210`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:212`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:216`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:218`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:226`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:227`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:235`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:236`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:252`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:253`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-private-key}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:253`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:254`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ssh-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:256`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:258`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.debug}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:260`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:269`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:269`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-forwarding-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-port}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-user}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.proxy-host}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:270`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:323`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.sync-delta-excludes}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:324`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:332`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.remote-protocol}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:346`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-mirror-options}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:359`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:361`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.ftp-post-sync-commands}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:368`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.artifacts}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:383`

### static-inline-injection (severity: high)

shell injection: expression "${{inputs.webhook}}" appears directly in run: block of step "Deploy"; move to env: map

Locations:

- `action.yml:385`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses

**Notes:**

Fixed all script-injection and static-inline-injection findings by moving all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block into a comprehensive env: block on the Deploy step. The shell script now references these values via environment variables (INPUT_REMOTE_PROTOCOL, GITHUB_SHA_VAL, etc.). List-type inputs (sync-delta-excludes, ftp-mirror-options) are tokenized using the xargs/while-read-NUL pattern to preserve argument boundaries. The only remaining ${{ }} expressions in the run: block are ${{ toJSON(env) }} and ${{ toJSON(inputs) }} which are display-only debug expressions. Pinned actions/upload-artifact@v4 to full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all script injection vulnerabilities in action.yml's Deploy step:
1. Replaced `echo "${{ toJSON(env) }}"` with `env` command and `echo "${{ toJSON(inputs) }}"` with `env | grep '^INPUT_'` to eliminate direct template expression interpolation in the run: block.
2. Replaced unquoted `echo "machine $INPUT_REMOTE_HOST login $INPUT_REMOTE_USER password ..."` with `printf 'machine %s login %s password %s\n' "$INPUT_REMOTE_HOST" "$INPUT_REMOTE_USER" "${input_remote_password}"` for safe netrc writing.
3. Replaced unquoted `$INPUT_FTP_OPTIONS` interpolation in lftprc with a separate `printf '%s\n' "$INPUT_FTP_OPTIONS"` append.
4. Replaced both unquoted `$INPUT_SSH_OPTIONS` interpolations with `printf 'set sftp:connect-program ... %s\n' "$INPUT_SSH_OPTIONS"` calls.
5. Replaced unquoted `open $INPUT_REMOTE_PROTOCOL://$INPUT_REMOTE_USER@$INPUT_REMOTE_HOST:$INPUT_REMOTE_PORT` with `printf 'open %s://%s@%s:%s\n' "$INPUT_REMOTE_PROTOCOL" "$INPUT_REMOTE_USER" "$INPUT_REMOTE_HOST" "$INPUT_REMOTE_PORT"`.
6. Replaced both unquoted `$INPUT_FTP_POST_SYNC_COMMANDS` interpolations in lftp -c strings by writing the commands to a temp file (`~/ftp_post_sync_commands.lftp`) and using lftp's `source` command to include them safely.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all script injection vulnerabilities in action.yml:

1. `${proxy_cmd}` (3 locations): Changed to `${proxy_cmd:+"$proxy_cmd"}` in apt-get install, proxy IP check curl command, and both lftp -c commands. This safely handles the empty case without passing an empty argument.

2. `${git_previous_commit}` (3 locations): Quoted as `"${git_previous_commit}"` in git cat-file -t, git diff, and git diff-tree commands.

3. `${local_path_unslash}` in git commands (2 locations): Quoted as `"${local_path_unslash}"` in git diff and git diff-tree commands.

4. `${local_path_unslash}` in sed with #e flag (2 locations): Created a shell-escaped version using `local_path_unslash_q=$(printf '%q' "$local_path_unslash")` and used `${local_path_unslash_q}` in the sed replacement string. The `#e` flag causes sed to execute the replacement as a shell command, making this the most critical injection vector.

5. `${ftp_mirror_opts[*]}` in lftp -c string: Changed to `${ftp_mirror_opts[*]+"${ftp_mirror_opts[@]}"}` for proper array expansion. The paths `${local_path_unslash}` and `${remote_path_unslash}` in the lftp mirror command are now wrapped in escaped double quotes within the lftp command string.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed the script injection vulnerability in action.yml at line 270. The `${local_path_slash}` variable (derived from user-controlled `inputs.local-path`) was used unquoted as a positional argument to `rsync`. Changed `${local_path_slash}` to `"${local_path_slash}"` to prevent shell metacharacter injection.

### Iteration 2

**Fixes applied:** hardcoded-credentials

**Notes:**

Replaced the hardcoded literal 'dummypassword' placeholder in action.yml (line 148) with a runtime-generated random hex value: `$(openssl rand -hex 16)`. This eliminates the hardcoded-credentials finding while preserving the functional behavior — lftp requires a non-empty password field in ~/.netrc even when SSH key-based authentication is used, so a random placeholder is generated at runtime instead of using a static literal string.

