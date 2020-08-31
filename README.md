# Todo Code Challenge
For this code challenge I split out the work into the following repositories:

- [todo client repo](https://github.com/bradford-hamilton/todo-client)
- [todo API repo](https://github.com/bradford-hamilton/todo-api)
- [todo API infrastructure](https://github.com/bradford-hamilton/todo-infra)

## Live Application
- http://t0d0client.s3-website-us-west-2.amazonaws.com

## Notes (if this were a production project):
### Communication Layer:
- Instead of going with a RESTful API right off the bat, I would dive way deeper into the goals of the project to figure out what makes the most sense in this layer - RESTful API vs. GraphQL vs. GRPC/protocol buffers, etc.
- Put domain and SSL in front of front/back ends. If it were `https://todos.com`, I would maybe put the load balanced api behind `https://api.todos.com`

### Persistance Layer:
- Set up or use a system for proper migrations.
- Ask product if historical data matters and if so consider something like a "deleted_at" column for todos. If it _really_ matters, then we could set that data up to sync to a data warehouse and keep our main active postgres instance nimble, while continuing to persist long term data that doesn't need frequent access.
- I'd like to explain some of the decisions I made around the "todo repository" pattern. The whole app doesn't follow this "hexagonal architecture" or "ports & adapters" pattern, however I really like some of the patterns they encourage.Using an interface here allows us to swap out data souces with a much higher degree of ease. For example, if we wanted to switch from a relational DB to a document store, we would implment the TodoRepository interface to work with that data appropriately. At that point, all other code and tests should validate a successful swap and should not need to be changed.
- Use context api with sql queries for timeouts.

### Error Handling:
- Error handling & http response messaging would be more thought out (input from product for things that bubble to the client).

### Testing
- More testing: continue with non-happy paths, errors, etc, as well as integration tests with a test db, etc and set those up as well on CI. This was the first time I've used Angular so I would dive into testing patterns/strategies there as well.

### DevOps
- Deployment would be well thought out in terms of where and what type of infrastructure. Discussing goals, customer needs, etc would help dictate which cloud provider/services to use.

### UI Layer
- Would love to make the todos drag and droppable... It would also be interesting to explore how to visualize "todo" vs "completed" vs "deleted".
