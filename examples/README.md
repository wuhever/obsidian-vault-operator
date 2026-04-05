# examples/

Optional demo content and sample SOPs the setup wizard can install into your vault.

## What's here

### `demo-content/`
A fictional AcmeCorp entity + sample project + sample idea. Useful for seeing the frontmatter schema and folder patterns in action. The wizard asks during setup whether to install this.

### `sop-examples/`
Working SOP files (vault health check, etc.) you can copy into your `06_Operations/` (or whatever your operations folder ends up being called after setup).

## How it's used

During `/setup`, the wizard asks:

> Would you like to install demo content so you can see the system in action? [y/N]

If yes, files from `examples/demo-content/` get copied into the appropriate numbered folders your wizard just created. If no, this folder is left untouched — delete it yourself when you don't need it anymore.

## Removing examples entirely

After setup, if you're confident you don't need these references:

```bash
rm -rf examples/
```

The template doesn't depend on this folder after setup — it's purely reference material.
