<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block directly interpolates dozens of ${{ }} expressions into shell commands (sub-rule a), allowing script injection. Attacker-controlled values include: `${{ github.event.head_commit.message }}` injected as a jq --arg shell argument; `${{ inputs.local-path }}` and `${{ inputs.remote-path }}` in path operations; `${{ inputs.remote-password }}`, `${{ inputs.remote-host }}`, `${{ inputs.remote-user }}`, `${{ inputs.remote-port }}`, `${{ inputs.remote-protocol }}` in shell comparisons and commands; `${{ inputs.sync }}` and `${{ github.event.inputs.sync }}` as unquoted shell assignments; `${{ inputs.ftp-options }}` injected into a heredoc written to ~/.lftprc; `${{ inputs.ssh-options }}` injected into an ssh connect-program string; `${{ inputs.proxy-forwarding-port }}`, `${{ inputs.proxy-port }}`, `${{ inputs.proxy-user }}`, `${{ inputs.proxy-host }}` injected directly into an ssh command; `${{ inputs.ftp-mirror-options }}` and `${{ inputs.ftp-post-sync-commands }}` injected into lftp -c command strings; `${{ inputs.sync-delta-excludes }}` injected into git diff; and `${{ github.event.before }}` / `${{ github.event.pull_request.base.sha }}` as unquoted shell assignments. Any of these can break out of their context and execute arbitrary shell commands.

Locations:

- `action.yml:76`
- `action.yml:83`
- `action.yml:100`
- `action.yml:104`
- `action.yml:107`
- `action.yml:110`
- `action.yml:113`
- `action.yml:116`
- `action.yml:119`
- `action.yml:122`
- `action.yml:125`
- `action.yml:128`
- `action.yml:155`
- `action.yml:175`
- `action.yml:195`
- `action.yml:210`
- `action.yml:230`
- `action.yml:245`
- `action.yml:260`

### unpinned-uses (severity: high)

The 'Upload artifacts' step uses `actions/upload-artifact@v4`, which is a mutable tag reference rather than a pinned 40-character commit SHA. This allows the referenced action to be silently updated or compromised without the workflow noticing. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:295`

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

1. All ${{ }} expressions moved from the Deploy step's run: block into a comprehensive env: block. This covers all inputs and github context values. The shell script now only uses plain $VAR_NAME references. List-type inputs (sync-delta-excludes, ftp-mirror-options) are tokenized with xargs into bash arrays for safe expansion. The ftp-options input is written via printf to ~/.lftprc. The ssh-options input is passed via printf format string. The ftp-post-sync-commands input is passed as a string into lftp -c (lftp command syntax, not shell). 2. actions/upload-artifact@v4 pinned to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02 # v4.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all four script-injection findings in hardened/action/action.yml:

1. **sed #e flag (lines 228-229)**: Replaced `sed --regexp-extended 's#(.*)#realpath ... $local_path_unslash \1#e'` with a safe `while IFS= read -r filepath; do realpath --canonicalize-missing --relative-to="${local_path_unslash}" "${filepath}"; done` loop. The #e flag caused sed to execute substitution results as shell commands.

2. **Unquoted ${git_previous_commit} (lines 214, 227, 228)**: Added double quotes around all uses in `git cat-file -t "${git_previous_commit}"`, `git diff "${git_previous_commit}"..`, and `git diff-tree "${git_previous_commit}"..`.

3. **Unquoted ${local_path_unslash}/${local_path_slash} (lines 227, 228, 235, 258, 269)**: Added double quotes around all uses in git diff `-- "${local_path_unslash}"`, git diff-tree `-- "${local_path_unslash}"`, rsync `"${local_path_slash}"`, and lftp commands.

4. **${post_sync_cmds} in lftp -c strings (lines 261, 274)**: Replaced `lftp -c "... ${post_sync_cmds}"` with writing lftp commands to a temp file using `mktemp` and `printf '%q'` for safe quoting of path variables, then running `lftp -f "${lftp_script}"`. This prevents user-controlled input from being injected into shell command strings while still allowing lftp commands to be passed through.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed unquoted shell variable expansions derived from user inputs:

1. `proxy_cmd`: Changed from a string variable (empty string or 'proxychains') to a bash array (`proxy_cmd=()` or `proxy_cmd=("proxychains")`). All 4 usages updated to `"${proxy_cmd[@]}"` — in the apt-get install command, the curl proxy IP check, and both lftp invocations (full sync and delta sync).

2. `apt_quiet`: Changed from a string variable (empty string or '--quiet --quiet') to a bash array (`apt_quiet=()` or `apt_quiet=("--quiet" "--quiet")`). Both usages in the apt-get commands updated to `"${apt_quiet[@]}"`.

Using bash arrays with `"${var[@]}"` expansion is the correct fix: when the array is empty it produces zero words (no spurious empty argument), and when populated each element is a properly quoted separate word, preventing word splitting and shell injection from user-controlled inputs.

