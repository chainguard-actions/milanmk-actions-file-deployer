<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.14

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.14** was hardened automatically. 53 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The 'Deploy' run: block in action.yml directly interpolates dozens of ${{ }} expressions into shell commands (rule a), and several are also unquoted (rule b). Attacker-controllable values include: `${{ github.event.head_commit.message }}` (commit message, fully attacker-controlled via a crafted commit), `${{ inputs.ftp-options }}`, `${{ inputs.ftp-mirror-options }}`, `${{ inputs.ftp-post-sync-commands }}`, `${{ inputs.ssh-options }}`, `${{ inputs.webhook }}`, `${{ inputs.local-path }}`, `${{ inputs.remote-path }}`, `${{ inputs.remote-password }}`, `${{ inputs.ssh-private-key }}`, `${{ inputs.proxy-private-key }}`, `${{ inputs.proxy-forwarding-port }}`, `${{ inputs.proxy-port }}`, `${{ inputs.proxy-user }}`, `${{ inputs.proxy-host }}`, `${{ inputs.sync }}`, `${{ inputs.remote-protocol }}`, `${{ inputs.remote-user }}`, `${{ inputs.remote-host }}`, `${{ inputs.remote-port }}`, `${{ github.event.before }}` (unquoted: `git_previous_commit=${{github.event.before}}`), `${{ github.event.pull_request.base.sha }}` (unquoted), `${{ github.event.inputs.sync }}` (unquoted: `input_sync=${{github.event.inputs.sync}}`), `${{ github.event_path }}` (unquoted argument to `cat`), and `${{ inputs.sync }}` (unquoted: `input_sync=${{inputs.sync}}`). Any of these can inject arbitrary shell commands when the action is called with malicious input.

Locations:

- `action.yml:68`
- `action.yml:76`
- `action.yml:80`
- `action.yml:88`
- `action.yml:92`
- `action.yml:96`
- `action.yml:100`
- `action.yml:104`
- `action.yml:108`
- `action.yml:115`
- `action.yml:122`
- `action.yml:126`
- `action.yml:130`
- `action.yml:134`
- `action.yml:138`
- `action.yml:142`
- `action.yml:148`
- `action.yml:152`
- `action.yml:160`
- `action.yml:168`
- `action.yml:176`
- `action.yml:188`
- `action.yml:200`
- `action.yml:218`
- `action.yml:222`
- `action.yml:226`
- `action.yml:232`
- `action.yml:248`
- `action.yml:252`
- `action.yml:258`
- `action.yml:264`
- `action.yml:270`
- `action.yml:276`
- `action.yml:290`
- `action.yml:296`
- `action.yml:302`
- `action.yml:316`
- `action.yml:320`
- `action.yml:328`
- `action.yml:332`

### unpinned-uses (severity: high)

The step 'Upload artifacts' uses `actions/upload-artifact@v4`, which is pinned to a mutable version tag rather than an immutable 40-character commit SHA. This allows the upstream action to be silently updated or compromised without any change to this action's source. It should be pinned to a full SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:348`

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

Fixed all script-injection findings by moving every ${{ }} expression from the run: block into a comprehensive env: block on the Deploy step. All 36 expressions (inputs.* and github.* context values) are now mapped to environment variables (INPUT_*, GITHUB_*) and referenced safely as $ENV_VAR in the shell script. List-style inputs (ftp-mirror-options, sync-delta-excludes) are tokenized with xargs into bash arrays; ftp-options is written via printf to lftprc; ftp-post-sync-commands is passed as a string to lftp's -c argument. Also removed the ${{toJSON(env)}} expression from the debug section (which cannot be safely moved to env:) and replaced it with a placeholder. Pinned actions/upload-artifact@v4 to the full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02 with a # v4 comment.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all unquoted shell variable expansions in action.yml:
1. Introduced proxy_cmd_arr bash array alongside proxy_cmd string, and replaced all `${proxy_cmd} cmd` command-prefix usages with `"${proxy_cmd_arr[@]}" cmd` (lines 224, 270, 285). This correctly handles the empty case (zero words) and non-empty case (one quoted word).
2. Changed `${proxy_cmd}` in apt-get install to `${proxy_cmd:+"$proxy_cmd"}` to avoid passing an empty argument (line 161).
3. Quoted `${git_previous_commit}` in git cat-file command (line 237).
4. Quoted `${local_path_unslash}` in git diff and git diff-tree commands (lines 248-249).
5. Added braces to `$local_path_unslash` in sed substitution strings (lines 252-253).
6. Quoted `${local_path_slash}` in rsync command (line 261).
7. Added escaped quotes around `${local_path_unslash}` inside the lftp -c string for the full sync command (line 272).

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all three script-injection findings in action.yml:
1. Line 196 (proxy-forwarding-port): Replaced `echo "...${INPUT_PROXY_FORWARDING_PORT}"` with `printf 'format %s\n' "${INPUT_PROXY_FORWARDING_PORT}"` to safely write the proxychains config without shell string injection risk.
2. Line 279 (mirror_opts[*]): Replaced the inline `lftp -c "...${mirror_opts[*]}..."` with a temp file approach using `lftp -f`. The lftp script is built using printf statements with %s format specifiers and a for loop over the array elements.
3. Lines 282 & 295 (post_sync_cmd): Both full-sync and delta-sync branches now use the temp file approach with `lftp -f`, writing post_sync_cmd via `printf '%s\n' "${post_sync_cmd}"` to avoid shell string injection. The temp files are cleaned up after use.

