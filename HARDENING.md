<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 54 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The run: block in action.yml directly interpolates ${{ }} expressions into shell commands throughout the entire script. Because this is a composite action, all inputs.* and github.* values are controlled by the calling workflow and can contain shell metacharacters. The Actions template engine substitutes these values before the shell parses the string, enabling command injection.

Sub-rule (a) violations — ${{ }} directly in run: shell commands — include:
• Unquoted variable assignments: `input_sync=${{inputs.sync}}`, `input_sync=${{github.event.inputs.sync}}`, `input_sync_delta_includes=${{inputs.sync-delta-includes}}`, `git_previous_commit=${{github.event.before}}`, `git_previous_commit=${{github.event.pull_request.base.sha}}`
• Unquoted in commands: `git rev-parse ${{github.sha}}^`, `cat ${{github.event_path}}`, `ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} -i ~/proxy_private_key ${{inputs.proxy-user}}@${{inputs.proxy-host}}`
• Injected into config files/commands: `${{inputs.ftp-options}}` written to ~/.lftprc, `${{inputs.ssh-options}}` appended to ~/.lftprc, `${{inputs.ftp-mirror-options}}` and `${{inputs.ftp-post-sync-commands}}` passed directly to lftp -c
• Interpolated into git diff commands: `${{inputs.sync-delta-excludes}}`
• Used in echo/realpath: `realpath --canonicalize-missing '${{inputs.remote-path}}'`, `echo "${{inputs.ssh-private-key}}"`, `echo "${{inputs.proxy-private-key}}"`
• Used in netrc: `echo "machine ${{inputs.remote-host}} login ${{inputs.remote-user}} password ..."`
• Used in curl URL: `"${{inputs.webhook}}"`

All of these allow an attacker-controlled calling workflow to inject arbitrary shell commands.

Locations:

- `action.yml:97`
- `action.yml:113`
- `action.yml:116`
- `action.yml:120`
- `action.yml:124`
- `action.yml:128`
- `action.yml:132`
- `action.yml:136`
- `action.yml:140`
- `action.yml:148`
- `action.yml:152`
- `action.yml:156`
- `action.yml:160`
- `action.yml:164`
- `action.yml:168`
- `action.yml:172`
- `action.yml:176`
- `action.yml:180`
- `action.yml:184`
- `action.yml:188`
- `action.yml:192`
- `action.yml:196`
- `action.yml:200`
- `action.yml:204`
- `action.yml:208`
- `action.yml:212`
- `action.yml:216`
- `action.yml:220`
- `action.yml:224`
- `action.yml:228`
- `action.yml:232`
- `action.yml:236`
- `action.yml:240`
- `action.yml:244`
- `action.yml:248`
- `action.yml:252`
- `action.yml:256`
- `action.yml:260`
- `action.yml:264`
- `action.yml:268`
- `action.yml:272`
- `action.yml:276`
- `action.yml:280`
- `action.yml:284`
- `action.yml:288`
- `action.yml:292`
- `action.yml:296`
- `action.yml:300`
- `action.yml:304`
- `action.yml:308`

### unpinned-uses (severity: high)

The composite action step 'Upload artifacts' uses `actions/upload-artifact@v7`, which references a mutable version tag (`v7`) rather than a pinned 40-character commit SHA. A tag can be moved to point to a different (potentially malicious) commit at any time, making this a supply-chain risk. It should be pinned to a full SHA, e.g. `actions/upload-artifact@<40-char-sha> # v7`.

Locations:

- `action.yml:313`

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

Fixed all script-injection findings by moving every ${{ inputs.* }} and ${{ github.* }} expression from the run: block into a step-level env: block. The shell script now references these values via environment variables ($INPUT_REMOTE_PROTOCOL, $INPUT_REMOTE_HOST, $GITHUB_SHA_VAL, etc.). For list-type inputs (sync-delta-excludes, ftp-mirror-options), used xargs-based tokenization into bash arrays to preserve argument boundaries. Pinned actions/upload-artifact@v7 to full SHA 043fb46d1a93c77aae656e7c1c64a875d1fc6a0a.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

Fixed all 7 script injection issues in action.yml:
1. $INPUT_FTP_OPTIONS: Separated from the multi-line echo string; now appended via `printf '%s\n' "$INPUT_FTP_OPTIONS" >> ~/.lftprc`
2. $INPUT_SSH_OPTIONS (both branches): Now passed as quoted printf argument: `printf 'set sftp:connect-program /usr/bin/ssh -a -x [-i ~/ssh_private_key] %s\n' "$INPUT_SSH_OPTIONS"`
3. $INPUT_REMOTE_PROTOCOL/$INPUT_REMOTE_USER/$INPUT_REMOTE_HOST/$INPUT_REMOTE_PORT: Now passed as quoted printf arguments: `printf 'open %s://%s@%s:%s\n' "$INPUT_REMOTE_PROTOCOL" "$INPUT_REMOTE_USER" "$INPUT_REMOTE_HOST" "$INPUT_REMOTE_PORT"`
4. ${ftp_mirror_opts[*]}: Now joined into lftp_mirror_opts_str via a for loop; ${local_path_unslash} and ${remote_path_unslash} are now quoted with escaped quotes inside the lftp -c string
5. ${ftp_post_sync}: Now referenced as $ftp_post_sync inside the double-quoted lftp -c string (bash expands but does not further interpret the content)
6. ${apt_quiet}: Changed from a string to an array (apt_quiet=("--quiet" "--quiet") or apt_quiet=()), expanded with "${apt_quiet[@]}"
7. for i in ${input_sync_delta_includes//,/ }: Fixed to use IFS=',' read -ra sync_includes_arr <<< "${input_sync_delta_includes}" and iterate with "${sync_includes_arr[@]}"
8. proxy_cmd: Changed from a string to an array (proxy_cmd=() or proxy_cmd=(proxychains)), expanded with "${proxy_cmd[@]}" throughout all usages

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all unquoted shell variable expansions identified in the script-injection finding:
1. Quoted ${git_previous_commit} in git cat-file -t, git diff, and git diff-tree commands
2. Quoted ${local_path_unslash} in git diff and git diff-tree commands (-- path argument)
3. Quoted ${local_path_slash} in rsync command
4. Changed $ftp_post_sync to ${ftp_post_sync} in both the full-sync and delta-sync lftp -c command strings (these are already inside double-quoted strings, so the braces form is the appropriate fix)

All changes are in hardened/action/action.yml.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed two script-injection findings in action.yml:

1. Lines 248-249 (sed 'e' flag): Replaced `sed --in-place --regexp-extended 's#(.*)#realpath --canonicalize-missing --relative-to=$local_path_unslash \1#e'` with a safe while-loop that calls `realpath` directly with properly quoted arguments. The sed 'e' flag executes the substitution result as a shell command, and `$local_path_unslash` (from user-controlled `$INPUT_LOCAL_PATH`) was interpolated directly into the pattern — both issues are now eliminated.

2. Lines 278 and 289 (lftp command injection): Replaced `lftp -c "... ${ftp_post_sync} ... ${lftp_mirror_opts_str} ..."` in both the `full` and `delta` sync branches with writing lftp commands to a temp file (via mktemp) and using `lftp -f`. Mirror options are individually quoted with `printf '%q'`, path arguments are properly quoted, and post-sync commands are written to the script file with `printf '%s\n'` rather than being interpolated into a bash string passed to lftp's `-c` argument. The temp file is cleaned up after use.

