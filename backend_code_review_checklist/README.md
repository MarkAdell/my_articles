# Backend Code Review Checklist

I have put together this checklist, which I believe will be applicable to most backend code reviews.

Some of these checks, such as Code Style, should ideally be enforced and detected in the CI pipeline. However, I have included them here for the sake of completeness.

You can use this checklist as a starting point and customize it to suit your specific needs.

## 1. Code Style

- Verify that the code adheres to the agreed-upon coding style guidelines.

## 2. Requirements

- Verify that the code fulfills the specified requirements.
- Verify that new code doesn't break any existing functionality.

## 3. Code Maintainability

- Verify that the code adheres to the clean code principles (or any other agreed-upon principles).

## 4. API Design

- Verify that any new APIs follow the agreed-upon API design guidelines.

## 5. Documentation and Comments

- Verify that complex logic or non-obvious decisions are covered by clear comments.
- Verify that any required internal or external code documentation is provided, depending on your agreed-upon documentation processes.

## 6. Error Handling

- Verify that exceptions are handled correctly and that error messages are informative.

## 7. Security

- Verify that inputs are validated properly.
- Verify that sensitive data (passwords, tokens) are securely stored and aren't leaked to logs.
- Examine the code for potential security vulnerabilities, such as SQL injection or authentication issues.

## 8. Dependencies

- Verify that dependencies are up-to-date and don't have known security vulnerabilities.
- Verify that any breaking changes are handled when updating dependencies.

## 9. Logging

- Verify that critical places in the code are covered by logs that are useful for debugging.
- Verify that logging adheres to the agreed-upon logging guidelines.

## 10. Testing

- Verify that the code is covered by the appropriate types of automated tests.

## 11. Performance

- Evaluate the code for performance issues (memory, CPU, network).
- Verify that database queries are optimized.

## 12. Version Control

- Verify that the agreed-upon version control workflow and practices are followed.

## 13. Spelling

- Verify that the spelling is correct, as this makes the code more searchable.

# Conclusion

I hope you found this checklist useful. Please feel free to suggest additional checks that you think are necessary.