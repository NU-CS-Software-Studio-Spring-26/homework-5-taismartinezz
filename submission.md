Part 3 - Ask Mode

Prompt used:
“Where is the todos index implemented? Include the files and line numbers. Do not suggest changes.”

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
“I want only the creator of a todo to mark it as done. Other logged-in users should still be able to see it. Make a plan with the files to change, tests to add, and any migrations. Do not write code.”

Cursor’s plan:

Add user_id and completed fields to todos if missing
Connect todos to users and assign current_user when creating todos
Add a toggle_completed action with an ownership check
Update _todo.html.erb so only owners can toggle todos
Add fixtures and controller tests

My edits:

Removed system tests because there is no auth system yet
Noted that some steps depend on having a User model first
Kept the migration, toggle action, and tests as the main tasks
Part 3 - Bad to Good Prompt

Bad prompt:
“Fix the bug in todos.”

Better prompt:
Add a flash message when a todo is deleted.

Files: todos_controller.rb and index.html.erb
Problem: No message appears after clicking “Destroy”
Expected result: Show “Todo was successfully deleted.”