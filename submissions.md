Part 3 - Ask Mode

Prompt used:
“Where in this codebase is the todos index implemented? Cite the exact files and line numbers. Do not propose changes.”

Cursor’s response included these files and locations:

config/routes.rb lines 1–3: resources :todos route
app/controllers/todos_controller.rb lines 4–7: index action using Todo.all
app/views/todos/index.html.erb lines 1–16: main HTML view
app/views/todos/index.json.jbuilder line 1: JSON response template
app/views/todos/_todo.html.erb: partial rendered by the index page
test/controllers/todos_controller_test.rb lines 8–11: test for the index action

Verification:
I checked all the files Cursor referenced and confirmed that the paths and line numbers were correct. The response was accurate and did not include any hallucinated files or code.