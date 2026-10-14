# Cosmic Quest Repository Instructions

## Architecture

- The entire application lives in `index.html`: semantic HTML, component styles, the question data, and all quiz behavior. Preserve this single-file, no-server, no-dependency architecture unless the task explicitly changes it.
- Quiz content is defined by the `questions` array. Each item has `category`, `question`, four `answers`, and a zero-based `correct` answer index.
- The UI has two mutually exclusive views: `#quiz-view` for questions and `#results` for the final score. `renderQuestion()` builds answer buttons, `selectAnswer()` locks and marks a response, and `showResults()` selects the final reaction from score thresholds.
- Runtime state is limited to `currentQuestion`, `score`, and `answered`. Cached DOM references live in the `elements` object.

## Run and Validation

- Open `index.html` directly in a browser with a `file://` URL; no install, build, server, test runner, or linter is configured.
- Validate quiz changes through the complete interaction flow: select an answer, confirm correct/wrong feedback and score behavior, advance through all 10 questions, verify the results screen, and restart.
- Also check keyboard focus, the narrow mobile layout at 430px or below, light and dark `prefers-color-scheme`, and `prefers-reduced-motion` when changing UI behavior or styles.

## Conventions

- Keep theme values in the light and dark `:root` custom-property blocks. Reuse those variables rather than adding hard-coded component colors.
- Answer state is represented by `.correct`, `.wrong`, and `.dimmed` classes. Correct answers use green feedback; wrong selections use red feedback and the `wrongShake` animation.
- Keep answer buttons accessible: use native buttons, preserve the `fieldset` label, expose status text through `role="status"`, update the progress bar's `aria-valuenow`, and retain visible `:focus-visible` styling.
- Respect the existing motion opt-out. New animations and transitions must be neutralized by the global `prefers-reduced-motion` rule.
- Keep the app centered in the existing narrow `.app` column and preserve the responsive stacked feedback controls on small screens.
- When adding or removing questions, derive counts, progress, and score displays from `questions.length`; update the progress bar's static `aria-valuemax` if the total changes.
