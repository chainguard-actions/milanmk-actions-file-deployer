<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.17

> This file was generated automatically by the hardening agent.

**Policy SHA:** `d636be7e43ef829af6e853da6b3c7566db9f72fe`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.17** was hardened automatically. 54 finding(s) were identified and resolved across 4 iteration(s).

## Findings Fixed

### script-injection (severity: high)

The `run:` block in action.yml directly interpolates dozens of `${{ }}` expressions into shell commands (sub-rule a), enabling script injection. Attacker-controllable inputs are substituted into the shell before it parses the script, allowing command injection via specially crafted input values. Examples include:
- `${{inputs.webhook}}` used as a URL in `curl --data ... "${{inputs.webhook}}"`
- `${{inputs.local-path}}` passed to `echo` and `realpath` unquoted
- `${{inputs.remote-path}}` passed to `realpath` in single-quoted context
- `${{inputs.remote-password}}` assigned directly: `input_remote_password="${{inputs.remote-password}}"`
- `${{inputs.sync}}` and `${{inputs.sync-delta-includes}}` assigned unquoted: `input_sync=${{inputs.sync}}`
- `${{inputs.ftp-options}}` written directly into ~/.lftprc config file
- `${{inputs.ftp-post-sync-commands}}` injected directly into `lftp -c "..."` command string
- `${{inputs.ftp-mirror-options}}` injected into `lftp -c "mirror ... ${{inputs.ftp-mirror-options}} ..."`
- `${{inputs.ssh-options}}` injected into `echo "set sftp:connect-program /usr/bin/ssh -a -x ${{inputs.ssh-options}}"`
- `${{inputs.proxy-forwarding-port}}`, `${{inputs.proxy-port}}`, `${{inputs.proxy-user}}`, `${{inputs.proxy-host}}` injected into `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}`
- `${{inputs.ssh-private-key}}` and `${{inputs.proxy-private-key}}` written via `echo "${{inputs.ssh-private-key}}" > ${key_ssh}`
- `${{github.event_name}}`, `${{github.event.inputs.sync}}`, `${{github.event.before}}`, `${{github.event.pull_request.base.sha}}`, `${{github.sha}}`, `${{github.event_path}}`, `${{github.repository}}`, `${{github.actor}}`, `${{github.event.head_commit.message}}` all interpolated directly into shell
- `${{inputs.sync-delta-excludes}}` injected into `git diff` command arguments
All of these must be moved to `env:` variables and referenced as properly double-quoted `"$VAR"` shell variables.

Locations:

- `action.yml:76`

### unpinned-uses (severity: high)

The composite action step `uses: actions/upload-artifact@v4` references the action by a mutable version tag (`v4`) rather than a full 40-character immutable commit SHA. This is vulnerable to supply-chain attacks if the tag is moved to point to a different (potentially malicious) commit. It should be pinned to a specific SHA, e.g. `actions/upload-artifact@65c4c4a1ddee5b72f698fdd19549f0f0fb45cf08 # v4`.

Locations:

- `action.yml:215`

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

Fixed all script injection findings by adding an env: block to the Deploy step with 37 environment variables covering all inputs and github context values (${{inputs.*}} and ${{github.*}}). All references in the run: block now use $VAR_NAME shell variable syntax instead of inline ${{ }} expressions. The two remaining ${{ }} expressions (toJSON(env) and toJSON(inputs)) are debug-only and not user-controlled injection risks. Also pinned actions/upload-artifact@v4 to the full commit SHA ea165f8d65b6e75b540449e92b4886f43607fa02.

### Iteration 2

**Fixes applied:** script-injection, hardcoded-credentials

**Notes:**

Fixed all findings in hardened/action/action.yml:

1. script-injection (sub-rule a): Moved `${{ toJSON(env) }}` and `${{ toJSON(inputs) }}` expressions out of the run: shell script into the step's env: block as GH_ENV_JSON and GH_INPUTS_JSON, then referenced them as plain env vars in the shell.

2. script-injection (sub-rule b): Fixed all unquoted variable expansions:
   - $INPUT_FTP_OPTIONS: Written separately with `printf '%s\n' "$INPUT_FTP_OPTIONS"` guarded by `[ -n ... ]`
   - $INPUT_SSH_OPTIONS: Passed as printf format argument: `printf 'set sftp:connect-program ... %s\n' "$INPUT_SSH_OPTIONS"`
   - $INPUT_REMOTE_PROTOCOL/USER/HOST/PORT: Each passed as separate printf format arguments
   - $INPUT_FTP_MIRROR_OPTIONS and $INPUT_FTP_POST_SYNC_COMMANDS: Replaced `lftp -c "..."` with writing commands to an lftp script file using properly quoted printf, then running `lftp -f "${lftp_script}"`
   - $INPUT_SYNC_DELTA_EXCLUDES: Tokenized with xargs into a bash array and expanded as `"${delta_excludes[@]}"`

3. hardcoded-credentials: Replaced `input_remote_password="dummypassword"` with `input_remote_password=""` to remove the hardcoded credential placeholder.

### Iteration 3

**Fixes applied:** script-injection

**Notes:**

Fixed all script-injection vulnerabilities in action.yml:
1. Converted `apt_quiet` string variable to bash array and expanded with `"${apt_quiet[@]}"` to prevent word-splitting injection.
2. Added `proxy_pkgs` array for the apt-get install command instead of unquoted `${proxy_cmd}`.
3. Replaced unquoted `for i in ${input_sync_delta_includes//,/ }` loop with xargs-based tokenization using a while/read loop.
4. Quoted `${git_previous_commit}` in git cat-file, git diff, and git diff-tree commands.
5. Quoted `${local_path_unslash}` in git diff and git diff-tree commands.
6. Replaced the dangerous `sed` with `e` flag (which executed shell commands with user-controlled input embedded in the sed expression) with safe `while IFS= read -r line; do realpath ... "$line"; done` loops.

### Iteration 4

**Fixes applied:** script-injection

**Notes:**

Fixed the unquoted variable `${local_path_slash}` (and also `$HOME/files_to_upload`) in the rsync command at action.yml line 248. Changed `rsync --verbose --files-from=$HOME/files_to_upload ${local_path_slash} ~/transfer_files/` to `rsync --verbose --files-from="$HOME/files_to_upload" "${local_path_slash}" ~/transfer_files/`. This prevents word-splitting and glob expansion on user-controlled input from `inputs.local-path`.

