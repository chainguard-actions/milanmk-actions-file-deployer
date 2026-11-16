<!-- markdownlint-disable -->

# Hardening Report: milanmk--actions-file-deployer/1.16

> This file was generated automatically by the hardening agent.

**Policy SHA:** `374911c4be584df24e6da57af2d990570ef0f859`

**Test Policy SHA:** `843adf9e4b8f85d0c08b27b9d0b09dd094b54702`

**Harden Agent Version:** `2`

Action **milanmk--actions-file-deployer/1.16** was hardened automatically. 54 finding(s) were identified and resolved across 3 iteration(s).

## Findings Fixed

### script-injection (severity: high)

Rule (a): the composite 'Deploy' step's run: block (starts at action.yml line 94) puts dozens of ${{ }} expressions straight into the bash script. Many of them are attacker-controlled. Examples: `--arg message "${{ github.event.head_commit.message }}"` and `Message: ${{github.event.head_commit.message}}`; `remote_path_unslash=$(realpath --canonicalize-missing '${{inputs.remote-path}}')`; `local_path_unslash=$(echo "${{inputs.local-path}}" | sed ...)`; `input_sync=${{inputs.sync}}` and `input_sync=${{github.event.inputs.sync}}` (unquoted); `echo "machine ${{inputs.remote-host}} login ${{inputs.remote-user}} ..."`; `echo "${{inputs.ssh-private-key}}"`; `echo "${{inputs.proxy-private-key}}"`; `${{inputs.ftp-options}}`; `${{inputs.ssh-options}}`; `ssh -A -D ${{inputs.proxy-forwarding-port}} ... ${{inputs.proxy-user}}@${{inputs.proxy-host}}`; `git_previous_commit=${{github.event.before}}` / `${{github.event.pull_request.base.sha}}`; `${{inputs.sync-delta-excludes}}`; `${{inputs.ftp-mirror-options}}`; `${{inputs.ftp-post-sync-commands}}`; `curl ... "${{inputs.webhook}}"`; `echo "${{toJSON(env)}}"` / `echo "${{toJSON(inputs)}}"`; `cat ${{github.event_path}}`; plus other github.* and inputs.* expressions. Fix: pass every value through the step's env: block and expand it double-quoted.

Locations:

- `action.yml:94`
- `action.yml:106`
- `action.yml:113`

### unpinned-uses (severity: high)

The composite step 'Upload artifacts' uses a mutable tag instead of a full 40-character commit SHA: `uses: actions/upload-artifact@v4`. The line number given is approximate: the reference is in the last step of action.yml.

Locations:

- `action.yml:380`

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

### prior-fix (severity: high)

Carried forward from this version's previous harden, which fixed it; fix it again unless the code no longer has the problem. The previous harden changed action.yml without recording a finding for it, and this analysis reported nothing there. Re-apply its security changes unless the code no longer needs them. The previous patch:
```diff
diff --git a/action.yml b/action.yml
index 0c28e9b..326e724 100644
--- a/action.yml
+++ b/action.yml
@@ -1,11 +1,8 @@
 name: "FTP/SFTP file deployer"
-
 description: "Fast and customizable deployment with parallel connections and proxy support. Deploy only changed files or do full sync."
-
 branding:
-  icon: "upload"  
+  icon: "upload"
   color: "black"
-
 inputs:
   remote-protocol:
     description: "Remote file transfer protocol (ftp, sftp)"
@@ -85,12 +82,67 @@ inputs:
   debug:
     description: "Enable debug information (true, false)"
     required: false
-
 runs:
   using: "composite"
   steps:
     - name: "Deploy"
       shell: bash
+      env:
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
+        INPUT_SSH_OPTIONS: ${{ inputs.ssh-options }}
+        INPUT_FTP_OPTIONS: ${{ inputs.ftp-options }}
+        INPUT_FTP_MIRROR_OPTIONS: ${{ inputs.ftp-mirror-options }}
+        INPUT_FTP_POST_SYNC_COMMANDS: ${{ inputs.ftp-post-sync-commands }}
+        INPUT_WEBHOOK: ${{ inputs.webhook }}
+        INPUT_ARTIFACTS: ${{ inputs.artifacts }}
+        INPUT_DEBUG: ${{ inputs.debug }}
+        GITHUB_REPOSITORY_NAME: ${{ github.repository }}
+        GITHUB_WORKFLOW_NAME: ${{ github.workflow }}
+        GITHUB_JOB_NAME: ${{ github.job }}
+        GITHUB_RUN_ID_VAL: ${{ github.run_id }}
+        GITHUB_REF_VAL: ${{ github.ref }}
+        GITHUB_EVENT_NAME: ${{ github.event_name }}
+        GITHUB_ACTOR_VAL: ${{ github.actor }}
+        GITHUB_HEAD_COMMIT_MESSAGE: ${{ github.event.head_commit.message }}
+        GITHUB_SHA_VAL: ${{ github.sha }}
+        GITHUB_EVENT_PATH_VAL: ${{ github.event_path }}
+        GITHUB_EVENT_INPUTS_SYNC: ${{ github.event.inputs.sync }}
+        GITHUB_EVENT_BEFORE: ${{ github.event.before }}
+        GITHUB_EVENT_PR_BASE_SHA: ${{ github.event.pull_request.base.sha }}
+        GITHUB_ENV_JSON: ${{ toJSON(env) }}
+        GITHUB_INPUTS_JSON: ${{ toJSON(inputs) }}
       run: |
         echo "::group::Initialization"
 
@@ -103,21 +155,21 @@ runs:
           local post_data=$(jq --null-input \
           --arg timestamp `date +%s` \
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
+          --arg repository "$GITHUB_REPOSITORY_NAME" \
+          --arg workflow "$GITHUB_WORKFLOW_NAME" \
+          --arg job "$GITHUB_JOB_NAME" \
+          --arg run_id "$GITHUB_RUN_ID_VAL" \
+          --arg ref "$GITHUB_REF_VAL" \
+          --arg event_name "$GITHUB_EVENT_NAME" \
+          --arg actor "$GITHUB_ACTOR_VAL" \
+          --arg message "$GITHUB_HEAD_COMMIT_MESSAGE" \
+          --arg revision "$GITHUB_SHA_VAL" \
           '{"timestamp": $timestamp, "status": $status, "repository": $repository, "workflow": $workflow, "job": $job, "run_id": $run_id, "ref": $ref, "event_name": $event_name, "actor": $actor, "message": 
... (truncated)
```

Locations:

- `action.yml`

## Iteration Notes

### Iteration 1

**Fixes applied:** script-injection, static-inline-injection, unpinned-uses, prior-fix

**Notes:**

Every ${{ }} expression in the 'Deploy' step's run: block (inputs.*, github.*, toJSON(env), toJSON(inputs), and github.event_path) now goes through the step's env: block, and the script reads each one as a double-quoted variable. Variables avoid reserved GITHUB_* names (e.g. GH_EVENT_NAME_VAL). sync-delta-excludes was pasted into the git diff commands unquoted, so the shell used to honor quotes inside it; it is now split into a bash array with the quote-aware xargs method, including the unmatched-quote check and the empty-value guard. Values that end up inside lftp/.lftprc/.netrc text strings (ftp-options, ssh-options, ftp-mirror-options, ftp-post-sync-commands) are now put into that text as variables inside the same double-quoted strings, so the generated text is unchanged. actions/upload-artifact@v4 is pinned to ea165f8d65b6e75b540449e92b4886f43607fa02 (# v4). This repeats the security changes from the previous harden.

### Iteration 2

**Fixes applied:** script-injection

**Notes:**

In the composite Deploy step: quoted ${local_path_unslash} in git diff / git diff-tree pathspecs; replaced the two `sed ... #e` invocations (which shell-executed each file name) with a while-read loop calling `realpath --canonicalize-missing --relative-to="$local_path_unslash" -- "$file"` per line, writing to a temp file then moving it back; quoted --files-from path and ${local_path_slash} in the rsync artifact copy.

### Iteration 1

**Fixes applied:** script-injection

**Notes:**

In action.yml's delta-sync lftp call, the awk argument inside the $(...) substitution is now `REMOTEPATH="\"${remote_path_slash}\""`. Before, `${remote_path_slash}` was expanded without quotes, so the shell split it into words and expanded it as a glob. Now it is double-quoted. The value awk receives is the same as before, literal quote characters included, so lftp's command text does not change. Nothing was run or tested.

