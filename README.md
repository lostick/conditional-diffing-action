# conditional-diffing

![build-test](https://github.com/lostick/conditional-diffing-action/workflows/build-test/badge.svg?branch=master)

This action can be used in a job step to filter paths based on git diff rules.  
The step sets `DIFF_DETECTED` environment variable as true or false, which can then be reused to conditionally run subsequent steps.

## Usage

```yaml
steps:
# Make sure to fetch all branches in order to do run git diff
- uses: actions/checkout@v2
- run: git fetch --no-tags --prune --depth=1 origin +refs/heads/master:refs/remotes/origin/master

- uses: lostick/conditional-diffing-action@v0.1.0

# This step uses DIFF_DETECTED env var to determine whether it needs to be run or not
- name: Setup go
  if: env.DIFF_DETECTED
  uses: actions/setup-go@v2
```
