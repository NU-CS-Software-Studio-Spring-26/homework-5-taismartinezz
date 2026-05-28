HW5 Submission:
Links
- hw5 branch: [https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/tree/hw5](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/tree/hw5)
- .cursorignore: [https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/.cursorignore](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/.cursorignore)
- AGENTS.md: [https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/AGENTS.md](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/AGENTS.md)
- rails-conventions.mdc: [https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/.cursor/rules/rails-conventions.mdc](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/.cursor/rules/rails-conventions.mdc)
- security.mdc: [https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/.cursor/rules/security.mdc](https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/blob/hw5/.cursor/rules/security.mdc)

Part 3 - Ask Mode

Prompt used:
"Where is the todos index implemented? Include the files and line numbers. Do not suggest changes."

Cursor found:

config/routes.rb lines 1–3: todos route
app/controllers/todos_controller.rb lines 4–7: index action
app/views/todos/index.html.erb lines 1–16: main view
app/views/todos/index.json.jbuilder line 1: JSON view
app/views/todos/_todo.html.erb: todo partial
test/controllers/todos_controller_test.rb lines 8–11: index test

Verification:
I checked the files and line numbers and everything was correct. No fake files or hallucinated code appeared.

Part 3 - Plan Mode

Prompt used:
"I want only the creator of a todo to mark it as done. Other logged-in users should still be able to see it. Make a plan with the files to change, tests to add, and any migrations. Do not write code."

Cursor's plan:

Add user_id and completed fields to todos if missing
Connect todos to users and assign current_user when creating todos
Add a toggle_completed action with an ownership check
Update _todo.html.erb so only owners can toggle todos
Add fixtures and controller tests

My edits:

Removed system tests because there is no auth system yet
Noted that some steps depend on having a User model first
Kept the migration, toggle action, and tests as the main tasks

Part 3 - Agent Mode

Prompt used:
"Implement only this one step: add a migration that adds a completed boolean 
column (default: false, null: false) to the todos table. Use bin/rails 
generate migration to create it. Do not touch any other files."

Commit: https://github.com/NU-CS-Software-Studio-Spring-26/homework-5-taismartinezz/commit/21de3d36db87611261258f60385fabc035df6cfa

Part 3 - Bad to Good Prompt

Bad prompt:
"Fix the bug in todos."

Better prompt:
1. Context: app/controllers/todos_controller.rb, app/views/todos/index.html.erb
2. Task: Add a flash message when a todo is deleted
3. Expected vs actual: After clicking "Destroy", the page should show "Todo was successfully deleted." but currently no message appears
4. Constraints: Only touch todos_controller.rb and index.html.erb. No new gems. Follow the existing flash notice pattern used in create/update.
5. Done when: Clicking Destroy shows the flash message on the index page and existing tests still pass.

Part 4 - Turbo Streams Explanation

Turbo Streams let a page update small parts of the screen without reloading the whole page.
They can replace, add, or remove content dynamically.

This is different from normal HTML because only part of the page changes instead of refreshing everything.

MIME type:
text/vnd.turbo-stream.html

Controller pattern:

respond_to do |format|
  format.html { redirect_to todos_path }
  format.turbo_stream
end

Example file:
app/views/todos/toggle_priority.turbo_stream.erb

Verification:
I verified the MIME type text/vnd.turbo-stream.html against the Turbo Streams handbook at turbo.hotwired.dev/handbook/streams, which confirms this is the correct Content-Type for Turbo Stream responses.

Turbo Streams in this project:
None yet. Turbo is installed, but there are no Turbo Stream responses in the project yet.

Part 4 - Acceptance Criteria
I want to mark a todo as high priority with a ❗.
Todo has a `high_priority` boolean attribute (default: false)
Every todo row on the index shows a ❗ button if high priority, or a faded ❕ if not
Clicking the toggle flips the priority and updates only that row (no full page reload)
The response Content-Type is `text/vnd.turbo-stream.html`
At least one automated test verifies the toggle returns a Turbo Stream

Part 4 - Plan

(a) Migration + model attribute
- Generate migration adding high_priority boolean (null: false, default: false) to todos
- Run bin/rails db:migrate
- Update test/fixtures/todos.yml with high_priority: false on :one and high_priority: true on :two

(b) Route + controller action
- Add member route: patch :toggle_high_priority in config/routes.rb
- Add toggle_high_priority action in todos_controller.rb that flips high_priority
- Add format.turbo_stream to respond_to block
- Add controller test asserting response media_type == "text/vnd.turbo-stream.html"

(c) Turbo Stream view + toggle button
- Create app/views/todos/toggle_high_priority.turbo_stream.erb using turbo_stream.replace
- Add ❗/❕ button_to in _todo.html.erb with data-turbo-stream on the form
- Add faded CSS class for low-priority state in application.css

My edits to the plan:
Removed the JSON response from the toggle action because this app does not use a JSON API
Skipped index filtering for now since the feature only needs a toggle action

Part 4 - Tests

Command: `bin/rails test`

Running 8 tests in a single process (parallelization threshold is 50)
Run options: --seed 6063
# Running:
........
Finished in 0.229736s, 34.8226 runs/s, 52.2339 assertions/s.
8 runs, 12 assertions, 0 failures, 0 errors, 0 skips

Part 4 - Pull Request
https://github.com/NU-CS-Software-Studio-Spring-26/nu-cs-software-studio-spring-26-homework-5-hw5/pull/14
