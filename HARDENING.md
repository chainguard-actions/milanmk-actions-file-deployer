<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.16

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.16** was hardened automatically. 53 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ }} expressions into shell commands without routing them through env: variables or quoting them safely. This violates sub-rule (a) for every occurrence and sub-rule (b) for unquoted expansions.

Attacker-controlled github.* values injected directly:
- `${{ github.event.head_commit.message }}` passed as a jq --arg value (commit message can contain shell metacharacters)
- `${{ github.event.inputs.sync }}` assigned unquoted: `input_sync=${{github.event.inputs.sync}}`
- `${{ github.event.before }}` assigned unquoted: `git_previous_commit=${{github.event.before}}`
- `${{ github.event.pull_request.base.sha }}` assigned unquoted
- `${{ github.sha }}^` passed to git rev-parse unquoted
- `${{ github.event_path }}` passed to cat unquoted
- `${{ github.actor }}`, `${{ github.ref }}`, `${{ github.repository }}`, `${{ github.workflow }}`, `${{ github.event_name }}` etc. all interpolated directly

Inputs.* values injected directly into shell:
- `${{inputs.webhook}}` used as a curl URL argument
- `${{inputs.local-path}}` inside echo/sed pipeline
- `${{inputs.remote-path}}` inside realpath call (single-quoted string still gets ${{ }} substituted before shell execution)
- `${{inputs.remote-password}}` assigned directly: `input_remote_password="${{inputs.remote-password}}"`
- `${{inputs.sync}}` assigned unquoted: `input_sync=${{inputs.sync}}`
- `${{inputs.remote-protocol}}`, `${{inputs.remote-host}}`, `${{inputs.remote-user}}`, `${{inputs.remote-port}}` used in comparisons and echoed into ~/.lftprc
- `${{inputs.ssh-private-key}}`, `${{inputs.proxy-private-key}}` echoed to key files
- `${{inputs.proxy-forwarding-port}}`, `${{inputs.proxy-port}}`, `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}` passed directly to ssh command: `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}`
- `${{inputs.ftp-options}}` injected into a heredoc written to ~/.lftprc (arbitrary lftp config injection)
- `${{inputs.ssh-options}}` injected into SSH connect-program string in ~/.lftprc
- `${{inputs.ftp-mirror-options}}` injected into lftp -c command string
- `${{inputs.ftp-post-sync-commands}}` injected into lftp -c command string (twice)
- `${{inputs.sync-delta-excludes}}` injected into git diff command
- `${{inputs.debug}}`, `${{inputs.artifacts}}` used in comparisons

Any of these values can contain shell metacharacters (`;`, `|`, `&`, `$(...)`, newlines) that will be interpreted by bash before any validation occurs.

Locations:

- `action.yml:68`
- `action.yml:78`
- `action.yml:88`
- `action.yml:97`
- `action.yml:104`
- `action.yml:107`
- `action.yml:110`
- `action.yml:116`
- `action.yml:117`
- `action.yml:122`
- `action.yml:155`
- `action.yml:160`
- `action.yml:163`
- `action.yml:173`
- `action.yml:193`
- `action.yml:195`
- `action.yml:197`
- `action.yml:212`
- `action.yml:237`
- `action.yml:240`
- `action.yml:247`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' references `actions/upload-artifact@v4`, which uses a mutable version tag rather than a full 40-character commit SHA. A tag can be moved by the upstream repository owner (or an attacker who compromises it) to point to a different, potentially malicious commit, enabling a supply-chain attack. It should be pinned to a specific SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:258`

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

1. Moved all ${{ }} expressions from the 'Deploy' run: block into an env: block. Created 36 environment variables covering all inputs (remote-protocol, remote-host, remote-port, remote-user, remote-password, ssh-private-key, proxy, proxy-host, proxy-port, proxy-forwarding-port, proxy-user, proxy-private-key, local-path, remote-path, sync, sync-delta-excludes, ssh-options, ftp-options, ftp-mirror-options, ftp-post-sync-commands, webhook, artifacts, debug) and all github context values (github.repository, github.workflow, github.job, github.run_id, github.ref, github.event_name, github.actor, github.event.head_commit.message, github.sha, github.event_path, github.event.before, github.event.pull_request.base.sha, github.event.inputs.sync). All references in the run: block now use $ENV_VAR_NAME shell variable syntax. 2. Pinned actions/upload-artifact@v4 to full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with # v4 comment.

### Iteration 2

**Fixes applied:** script-injection, suspicious-run-content, hardcoded-credentials

**Notes:**

Fixed all three findings in action.yml:

1. hardcoded-credentials (line 165): Replaced literal 'dummypassword' fallback with '$(openssl rand -hex 16)' to generate a random placeholder at runtime.

2. script-injection (lines 195-284): Fixed all 5 injection points:
   - $INPUT_FTP_OPTIONS: Now written with printf '%s\n' "$INPUT_FTP_OPTIONS" (properly quoted)
   - $INPUT_SSH_OPTIONS: Now passed as a separate printf format argument "$INPUT_SSH_OPTIONS" (properly quoted)
   - ${INPUT_SYNC_DELTA_EXCLUDES}: Tokenized into a bash array using xargs NUL-delimited read loop, expanded as "${sync_delta_excludes[@]}"
   - $INPUT_FTP_MIRROR_OPTIONS: Tokenized into a bash array using xargs, each token printed separately into lftp script file
   - $INPUT_FTP_POST_SYNC_COMMANDS: Written with printf '%s\n' "$INPUT_FTP_POST_SYNC_COMMANDS" into lftp script file
   Switched from 'lftp -c "..."' to writing commands to a script file and using 'lftp -f scriptfile' to eliminate shell-level injection risk.

3. suspicious-run-content (line 148): Added HTTPS-only URL validation in send_webhook() using a case statement that rejects non-HTTPS webhook URLs with a warning, preventing exfiltration to arbitrary protocols.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed the script-injection finding (Sub-rule b) by double-quoting all unquoted variable expansions of untrusted data in the 'Deploy' run block:
1. `${git_previous_commit}` → `"${git_previous_commit}"` in `git cat-file -t`, `git diff`, and `git diff-tree` commands
2. `${local_path_unslash}` → `"${local_path_unslash}"` in `git diff`, `git diff-tree`, and `sed --relative-to=` arguments
3. `${local_path_slash}` → `"${local_path_slash}"` in the `rsync` command

For the suspicious-run-content finding (outbound-exfiltration): The webhook feature is an intentional design of this action (sending deployment status notifications). The code already enforces HTTPS-only URLs via a `case "$INPUT_WEBHOOK" in https://*) ... esac` check, which prevents HTTP exfiltration. The `post_data` is constructed safely using `jq --arg` (preventing injection). This is a legitimate webhook notification feature with existing HTTPS enforcement, not a security vulnerability that can be fixed without removing the feature entirely.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

Fixed all four script-injection locations in action.yml by converting `proxy_cmd` and `apt_quiet` from plain string variables to bash arrays. `proxy_cmd` is now initialized as `proxy_cmd=()` (empty) or `proxy_cmd=("proxychains")` (when proxy is enabled), and expanded safely as `"${proxy_cmd[@]}"` in all four locations: the apt-get install command (line 175), the proxy IP address check command substitution (line 232), and both lftp execution calls (lines 282 and 352). Similarly, `apt_quiet` is now `apt_quiet=(--quiet --quiet)` or `apt_quiet=()` and expanded as `"${apt_quiet[@]}"`. Using array expansion with `[@]` ensures that when the array is empty, no argument is passed (preventing injection), and when set, each element is a separate properly-quoted argument.

