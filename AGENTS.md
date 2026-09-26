# Lost Pixel

## Map and development

`src/bin.ts` is the CLI; `src/runner.ts` orchestrates it; `src/shots/`, `src/crawler/`, and `src/compare/` handle capture and comparison. `src/upload.ts`/`src/api.ts` are the remote service boundary. `fixtures/` and `.lostpixel/` contain visual evidence; `examples/` supplies framework-specific targets; `action.yml`, `entrypoint.sh`, and `Dockerfile` package the GitHub Action.

Use npm and `package-lock.json`: `npm ci`. `.nvmrc` and PR CI use Node 18, and the manifest declares Node >=18. `npm run dev` runs the CLI, not a web development server; it uses the current target's configuration and may capture external pages or upload results. Read that configuration before a runtime smoke check.

## Verification

Run focused Jest cases with `npm test -- <test-path>`, `npm run lint` (XO plus unused-export checks), and `npm run build` (TypeScript compilation) for relevant code changes. Follow `CONTRIBUTING.md` to build a local example and run `npx ts-node ../../src/bin.ts` from its directory. Storybook example build scripts require Docker and install dependencies inside mounted example folders; `npm run test-on-examples` requires the examples and CLI to be built first.

Inspect generated comparison images for capture/diff changes. Baseline replacement must reflect the intended visual change, not hide a regression. Keep local fixture evidence distinct from cloud uploads, release tasks, and real browser/service availability; preserve the applicable authorization for those external effects.

## Finishing work

Follow the nearby implementation and keep changes within the requested scope. Carry authorized changes through the relevant checks, fixing failures caused by the change. For a bug, reproduce the affected behavior and add a focused regression check when useful. Make routine reversible choices without another approval; ask only when missing information materially changes correctness, scope, or authorization, and name the exact source of any blocking rule. Report what changed, checks actually run, and concrete unverified behavior; repeat checks when new edits or evidence warrant it.
