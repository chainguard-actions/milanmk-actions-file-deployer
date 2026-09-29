<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.15

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.15** was hardened automatically. 53 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ inputs.* }} and ${{ github.* }} expressions into shell commands (sub-rule a), allowing an attacker who controls those values to inject arbitrary shell commands. Representative violations include:
- `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)` — inputs.local-path interpolated into shell
- `remote_path_unslash=$(realpath --canonicalize-missing '${{inputs.remote-path}}')` — inputs.remote-path interpolated (single-quoting the outer string does not prevent template expansion)
- `input_remote_password="${{inputs.remote-password}}"` — password directly in shell
- `input_sync=${{inputs.sync}}` — unquoted, no word-splitting protection
- `input_sync=${{github.event.inputs.sync}}` — unquoted github context
- `${{inputs.ftp-options}}` written verbatim into ~/.lftprc
- `echo "set sftp:connect-program /usr/bin/ssh -a -x ${{inputs.ssh-options}}"` — ssh-options injected into lftp config
- `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}` — multiple inputs directly in ssh command
- `${{inputs.ftp-mirror-options}}` and `${{inputs.ftp-post-sync-commands}}` injected into lftp -c command string
- `git_previous_commit=${{github.event.before}}` and `${{github.event.pull_request.base.sha}}` — unquoted github event data
- `git diff ... ${{inputs.sync-delta-excludes}}` — unquoted input in git command
- `${{github.event.head_commit.message}}` passed as jq --arg value (commit message can contain shell metacharacters that break the surrounding jq invocation)
Every one of these is a direct ${{ }} interpolation inside a run: shell script.

Locations:

- `action.yml:68`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v4`, which uses a mutable version tag instead of a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, enabling a supply-chain attack. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:215`

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

Fixed all script-injection findings by moving every ${{ inputs.* }} and ${{ github.* }} expression from the run: shell script into an env: block on the Deploy step. The shell script now uses only ${ENV_VAR} references. Special handling was applied for list-style inputs (sync-delta-excludes, ftp-mirror-options) using xargs tokenization into bash arrays. The ftp-options, ssh-options, and connection parameters are written to config files via printf format strings. Pinned actions/upload-artifact@v4 to full SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 5 script-injection findings in hardened/action/action.yml:

1. **apt_quiet/proxy_cmd unquoted (line 148)**: Converted `apt_quiet` to a bash array (`apt_quiet=(--quiet --quiet)` / `apt_quiet=()`), expanded as `"${apt_quiet[@]}"`. Converted `proxy_cmd` to a bash array (`proxy_cmd=()` / `proxy_cmd=(proxychains)`), expanded as `"${proxy_cmd[@]}"` in the apt-get install line.

2. **proxy_cmd unquoted as command prefix (lines 196, 278, 291)**: All three `${proxy_cmd}` command-prefix usages updated to `"${proxy_cmd[@]}"` array expansion.

3. **git_previous_commit unquoted (line 231)**: Added double quotes: `git cat-file -t "${git_previous_commit}"`.

4. **sed with 'e' flag (lines 248, 249)**: Replaced the dangerous `sed ... #e` pattern (which executes shell commands) with safe `while IFS= read -r _f; do realpath ... "${_f}"; done < input > output.tmp && mv output.tmp output` loops.

5. **Unquoted variables in lftp command strings (lines 278, 291)**: Restructured both lftp invocations to write commands to a mktemp script file using `printf '%q'` for path variables and `printf '%s\n'` for user-controlled post-sync commands, then execute with `lftp -f scriptfile`. This prevents shell expansion of user-controlled content and properly quotes all path arguments within the lftp command script.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed the script injection vulnerability in the 'Deploy' step's rsync command. The variable `${local_path_slash}` (derived from `inputs.local-path` via `INPUT_LOCAL_PATH`) was expanded unquoted in the rsync command: `rsync --verbose --files-from=$HOME/files_to_upload ${local_path_slash} ~/transfer_files/`. An attacker-controlled `inputs.local-path` value containing shell metacharacters could enable command injection. Fixed by adding double quotes: `rsync --verbose --files-from=$HOME/files_to_upload "${local_path_slash}" ~/transfer_files/`.

