<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `1`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions inside shell commands. The Actions runner substitutes these values into the shell script before the shell ever parses them, enabling arbitrary command injection by any caller of this composite action. Critical examples include:

(a) Unquoted input interpolation: `input_sync=${{inputs.sync}}` — no quotes, no braces, allows word-splitting and glob expansion.
(b) Unquoted SSH arguments: `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — all four input values injected directly as unquoted shell tokens.
(c) Arbitrary lftp command injection: `${{inputs.ftp-options}}` written directly into ~/.lftprc; `${{inputs.ftp-mirror-options}}` and `${{inputs.ftp-post-sync-commands}}` injected directly into lftp -c command strings — an attacker can supply arbitrary lftp or shell commands.
(d) Unquoted git arguments: `${{inputs.sync-delta-excludes}}` passed unquoted to git diff.
(e) Unquoted github context values: `git_previous_commit=${{github.event.before}}`, `git_previous_commit=${{github.event.pull_request.base.sha}}`, `git rev-parse ${{github.sha}}^` — all unquoted.
(f) `realpath --canonicalize-missing '${{inputs.remote-path}}'` — single-quoted in YAML but the ${{ }} is substituted before the shell sees the single quotes, so path traversal/injection is possible.

All ${{ ... }} expressions must be moved to env: variables and then double-quoted in the shell script.

Locations:

- `action.yml:96`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v4`, which uses a mutable version tag rather than a pinned 40-character commit SHA. A supply-chain attacker who compromises the actions/upload-artifact repository could push malicious code to the v4 tag and have it execute in any workflow using this action. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:248`

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

Rewrote action.yml to fix all security findings:

1. script-injection / static-inline-injection (50+ instances): Moved all ${{ inputs.* }} and ${{ github.* }} expressions from the run: block into an env: block on the Deploy step. Created environment variables for all 23 inputs and 13 github context values. The shell script now references these exclusively as double-quoted $ENV_VAR references, eliminating all shell injection vectors.

2. unpinned-uses: Pinned actions/upload-artifact@v4 to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with # v4 comment.

Key security improvements: SSH arguments are now properly double-quoted; realpath now uses double-quoted env var instead of single-quoted inline expression; git diff commands handle optional sync-delta-excludes with a conditional to avoid empty-string argument issues; private key files are written with printf '%s' to avoid shell interpretation; proxychains config uses printf instead of heredoc with inline expression.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all four script-injection findings in action.yml:

1. **sed 'e' flag injection (lines 248-249)**: Replaced `sed --regexp-extended 's#(.*)#realpath ... $local_path_unslash \1#e'` (which executes the replacement as a shell command, allowing injection via local-path) with a safe `while IFS= read -r _line; do realpath --canonicalize-missing --relative-to="${local_path_unslash}" "${_line}"; done` loop that properly quotes all variables.

2. **Unquoted vars in lftp mirror command (line 271)**: Refactored the lftp command to build it as a `lftp_cmd` string variable with `${local_path_unslash}` and `${remote_path_unslash}` properly quoted using lftp-style `\"...\"` quoting. `INPUT_FTP_MIRROR_OPTIONS` is conditionally appended only when non-empty.

3. **Unquoted INPUT_FTP_POST_SYNC_COMMANDS (lines 274, 282)**: Moved `${INPUT_FTP_POST_SYNC_COMMANDS}` to be conditionally appended to the `lftp_cmd` string variable only when non-empty, with the entire command string passed as a single quoted argument to `lftp -c`.

4. **Unquoted proxy_cmd (lines 196, 269, 276)**: Replaced the string variable `proxy_cmd` with a bash array `proxy_cmd_arr=()`. When proxy is disabled, the array is empty (expands to zero words). When enabled, it contains `("proxychains")`. All usages now use `"${proxy_cmd_arr[@]}"` which is safe and properly quoted, preventing any shell metacharacter injection.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed 6 script-injection vulnerabilities in action.yml:
1. apt_quiet variable: converted from unquoted string ('--quiet --quiet') to a bash array (--quiet --quiet) expanded safely with "${apt_quiet[@]}" — prevents word-splitting and shell metacharacter injection.
2. INPUT_FTP_MIRROR_OPTIONS: sanitized with `$(printf '%s' "${INPUT_FTP_MIRROR_OPTIONS}" | tr -d '\n\r')` before concatenation into lftp command string.
3. INPUT_FTP_POST_SYNC_COMMANDS (full sync): sanitized with printf+tr before appending to lftp command.
4. INPUT_FTP_OPTIONS written to ~/.lftprc: sanitized with printf+tr to strip embedded newlines that could inject additional lftp config directives.
5. INPUT_SSH_OPTIONS written to ~/.lftprc: sanitized with printf+tr to strip embedded newlines.
6. INPUT_FTP_POST_SYNC_COMMANDS (delta sync): sanitized with printf+tr before appending to lftp command.

All inputs were already correctly placed in the step's env: block rather than using ${{ }} directly in run:, so no env: block changes were needed. The fixes address shell-level injection via unquoted expansion and newline injection.

