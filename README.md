This repo demonstrates a bug with github action's composite actions feature.

On the main branch it has two github actions workflows, called 'working-action' and 'broken-action'.  Both are called by dispatch and just print a strings.

Both actions use a composite-action that calls `actions/setup-node@v4` which has a `Post Run` step.   

There is a separate branch called `no-composite-action` which does not have the composite action in it.

`broken-action` switches to the `no-composite-action` branch as it goes.  the workflow fails because it tries to run the `Post Run` step of the composite action but it can't find the composite action, having switched branches.

The error reads: 
 Can't find 'action.yml', 'action.yaml' or 'Dockerfile' under '/home/runner/work/composite-action-post-run-bug/composite-action-post-run-bug/.github/simple-composite-action'. Did you forget to run actions/checkout before running your local action?
