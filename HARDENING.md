<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.18

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.18** was hardened automatically. 55 finding(s) were identified and resolved across 2 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (a): the composite 'Deploy' step's run: block puts dozens of ${{ }} expressions straight into the bash script. Some are attacker-controllable, such as github.event.head_commit.message (in the jq --arg message and in the 'Message:' echo) and github.event.inputs.sync ('input_sync=${{github.event.inputs.sync}}', unquoted). Many inputs.* values are also used directly and unquoted, for example: input_sync=${{inputs.sync}}, input_sync_delta_includes=${{inputs.sync-delta-includes}}, '${{inputs.ftp-options}}', '${{inputs.ssh-options}}', 'ssh -A -D ${{inputs.proxy-forwarding-port}} -f -N -p ${{inputs.proxy-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}', '${{inputs.sync-delta-excludes}}', '${{inputs.ftp-mirror-options}}', '${{inputs.ftp-post-sync-commands}}', "${{inputs.webhook}}", echo "${{inputs.ssh-private-key}}", echo "${{toJSON(env)}}", 'cat ${{github.event_path}}', and 'git_previous_commit=${{github.event.before}}'. Commit messages and inputs can contain quotes, $(...) or ';', so these values can run arbitrary shell commands. Fix: map each value to an env: variable and always double-quote it in the script.

Locations:

- `action.yml:97`
- `action.yml:119`
- `action.yml:123`

### unpinned-uses (severity: high)

The composite step 'Upload artifacts' references an action by a mutable tag instead of a full commit SHA: 'uses: actions/upload-artifact@v7'. Pin it to a 40-character commit SHA.

Locations:

- `action.yml:445`

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

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 86fc43a..5e3188d 100644
--- a/action.yml
+++ b/action.yml
@@ -92,8 +92,65 @@ inputs:
 runs:
   using: "composite"
   steps:
     - name: "Deploy"
       shell: bash
+      env:
+        GH_REPOSITORY: ${{ github.repository }}
+        GH_WORKFLOW: ${{ github.workflow }}
+        GH_JOB: ${{ github.job }}
+        GH_RUN_ID: ${{ github.run_id }}
+        GH_REF: ${{ github.ref }}
+        GH_EVENT_NAME: ${{ github.event_name }}
+        GH_ACTOR: ${{ github.actor }}
+        GH_HEAD_COMMIT_MESSAGE: ${{ github.event.head_commit.message }}
+        GH_SHA: ${{ github.sha }}
+        GH_EVENT_PATH: ${{ github.event_path }}
+        GH_EVENT_BEFORE: ${{ github.event.before }}
+        GH_PR_BASE_SHA: ${{ github.event.pull_request.base.sha }}
+        GH_EVENT_INPUTS_SYNC: ${{ github.event.inputs.sync }}
+        DEBUG_ENV_JSON: ${{ toJSON(env) }}
+        DEBUG_INPUTS_JSON: ${{ toJSON(inputs) }}
+        INPUT_REMOTE_PROTOCOL: ${{ inputs.remote-protocol }}
+        INPUT_REMOTE_HOST: ${{ inputs.remote-host }}
+        INPUT_REMOTE_PORT: ${{ inputs.remote-port }}
+        INPUT_REMOTE_USER: ${{ inputs.remote-user }}
+        INPUT_REMOTE_PASSWORD: ${{ inputs.remote-password }}
+        INPUT_SSH_PRIVATE_KEY: ${{ inputs.ssh-private-key }}
+        INPUT_PROXY: ${{ inputs.proxy }}
+        INPUT_PROXY_HOST: ${{ inputs.proxy-host }}
+        INPUT_PROXY_PORT: ${{ inputs.proxy-port }}
+        INPUT_PROXY_FORWARDING_PORT: ${{ inputs.proxy-forwarding-port }}
+        INPUT_PROXY_USER: ${{ inputs.proxy-user }}
+        INPUT_PROXY_PRIVATE_KEY: ${{ inputs.proxy-private-key }}
+        INPUT_LOCAL_PATH: ${{ inputs.local-path }}
+        INPUT_REMOTE_PATH: ${{ inputs.remote-path }}
+        INPUT_SYNC: ${{ inputs.sync }}
+        INPUT_SYNC_DELTA_EXCLUDES: ${{ inputs.sync-delta-excludes }}
+        INPUT_SYNC_DELTA_INCLUDES: ${{ inputs.sync-delta-includes }}
+        INPUT_SSH_OPTIONS: ${{ inputs.ssh-options }}
+        INPUT_FTP_OPTIONS: ${{ inputs.ftp-options }}
+        INPUT_FTP_MIRROR_OPTIONS: ${{ inputs.ftp-mirror-options }}
+        INPUT_FTP_POST_SYNC_COMMANDS: ${{ inputs.ftp-post-sync-commands }}
+        INPUT_WEBHOOK: ${{ inputs.webhook }}
+        INPUT_ARTIFACTS: ${{ inputs.artifacts }}
+        INPUT_DEBUG: ${{ inputs.debug }}
       run: |
         echo "::group::Initialization"
 
@@ -109,21 +166,21 @@ runs:
           post_data=$(jq --null-input \
           --arg timestamp "$(date +%s)" \
           --arg status "${status}" \
-          --arg repository "${{ github.repository }}" \
-          --arg workflow "${{ github.workflow }}" \
-          --arg job "${{ github.job }}" \
-          --arg run_id "${{ github.run_id }}" \
-          --arg ref "${{ github.ref }}" \
-          --arg event_name "${{ github.event_name }}" \
-          --arg actor "${{ github.actor }}" \
-          --arg message "${{ github.event.head_commit.message }}" \
-          --arg revision "${{ github.sha }}" \
+          --arg repository "${GH_REPOSITORY}" \
+          --arg workflow "${GH_WORKFLOW}" \
+          --arg job "${GH_JOB}" \
+          --arg run_id "${GH_RUN_ID}" \
+          --arg ref "${GH_REF}" \
+          --arg event_name "${GH_EVENT_NAME}" \
+          --arg actor "${GH_ACTOR}" \
+          --arg message "${GH_HEAD_COMMIT_MESSAGE}" \
+          --arg revision "${GH_SHA}" \
           '{"timestamp": $timestamp, "status": $status, "repository": $repository, "workflow": $workflow, "job": $job, "run_id": $run_id, "ref": $ref, "event_name": $event_name, "actor": $actor, "message": $message, "revision": $revision}')
 
-          curl --data "${post_data}" --header "Content-Type: application/json" --max-time 30 --show-error --silent --user-agent "GitHub Workflow" "${{inputs.webhook}}"
+          curl --data "${post_data}" --header "Content-Type: application/json" --max-time 30 --show-error --silent --user-agent "GitHub Workflow" "${INPUT_WEBHOOK}"
         }
 
-        [ -n "${{inputs.webhook}}" ] && echo "Webhook notification (start): $(send_webhook "start")"
+        [ -n "${INPUT_WEBHOOK}" 
... (truncated)
```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses, prior-fix

**Notes:**

Moved every ${{ }} expression in the composite 'Deploy' step into its env: block (github context values, toJSON(env)/toJSON(inputs), and all inputs.*). The script now uses them as double-quoted shell variables. Values that land inside generated config or lftp command strings (ftp-options, ssh-options, ftp-mirror-options, ftp-post-sync-commands) now expand once as plain text, so the shell no longer evaluates them. sync-delta-excludes was pasted unquoted into git diff, so it is split into an array with the quote-aware xargs method to keep upstream's argument splitting. sync-delta-includes still uses upstream's comma/whitespace loop. Private keys are written with printf. github.event.before, the PR base sha and github.sha are quoted. I pinned actions/upload-artifact@v7 to cf430e030ddbb5b0abf93d22962f4752f3646cd9. This re-applies the previous harden's env-mapping changes.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

I fixed all five script-injection points in the 'Deploy' step of action.yml. Nothing has been run or tested; the changes were checked by reading only.

1. Quoted "${git_previous_commit}" in the `git cat-file` check.
2. Quoted "${local_path_unslash}" in the `git diff` and `git diff-tree` path filters. This input is a single path, not a list.
3. sync-delta-includes is still split the way upstream split it (on commas and whitespace, with glob expansion), but the split now builds a bash array first (`sync_delta_includes=(${input_sync_delta_includes//,/ })`) and the loop runs over "${array[@]}". The array assignment is still an unquoted expansion. That is on purpose so globs like dir/* keep working; it can't run commands (no `$(...)`, `;` or backticks are evaluated). A later scan may flag that line again.
4. Removed the two `sed ... #e` commands, which ran each built line as a shell command. A small helper now reads each file list line by line and calls `realpath --canonicalize-missing --relative-to="${local_path_unslash}" -- "$f"` directly, then replaces the list with a temp file. File names and local-path are never handed to a shell now. Two small behaviour changes: blank lines are skipped, and a file name containing spaces is now handled correctly instead of being split into words.
5. Quoted "$HOME/files_to_upload" and "${local_path_slash}" in the `rsync` artifact copy.

