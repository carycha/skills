# API Design Checklist

Before shipping a new endpoint, verify the following:

- [ ] **Naming**: Resource URL follows naming conventions (plural, kebab-case, no verbs).
- [ ] **Methods**: Correct HTTP method used (GET for reads, POST for creates, etc.).
- [ ] **Status Codes**: Appropriate status codes returned (not 200 for everything).
- [ ] **Validation**: Input validated with schema (Zod, Pydantic, Bean Validation).
- [ ] **Errors**: Error responses follow standard format with codes and messages.
- [ ] **Pagination**: Implemented for list endpoints (cursor or offset).
- [ ] **AuthN**: Authentication required (or explicitly marked as public).
- [ ] **AuthZ**: Authorization checked (user can only access their own resources).
- [ ] **Rate Limiting**: Configured appropriately for the tier.
- [ ] **Security**: Response does not leak internal details (stack traces, SQL errors).
- [ ] **Consistency**: Naming consistent with existing endpoints (camelCase vs snake_case).
- [ ] **Docs**: Documented (OpenAPI/Swagger spec updated).
