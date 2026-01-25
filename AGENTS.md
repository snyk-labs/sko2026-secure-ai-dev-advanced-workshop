# AI Agent Instructions

This file provides instructions for AI coding agents (Cursor, Windsurf, Kilo Code, etc.) working on this project.

## Code Quality Standards

- All functions must have JSDoc comments describing parameters, return values, and purpose
- Use async/await for asynchronous operations, never raw Promises with .then()
- Validate all inputs before processing (check types, required fields, format)
- Write unit tests for all new functions
- Use meaningful variable and function names that describe their purpose
- Keep functions small and focused on a single responsibility

## Security Guidelines

- Never log sensitive data (passwords, tokens, API keys, PII)
- Use parameterized queries for database operations to prevent SQL injection
- Validate and sanitize all user input before processing
- Use secure password hashing (bcrypt, argon2) with appropriate cost factors
- Always use the latest versions of all open source dependencies
- Set appropriate HTTP security headers (CORS, Content-Security-Policy, etc.)
- Use HTTPS in production environments
- Implement rate limiting on authentication endpoints

## Compliance Guidelines

- Never use GPL-licensed dependencies (use MIT, Apache 2.0, or BSD licenses)
- Document all third-party dependencies and their licenses
- Ensure data handling complies with privacy regulations (GDPR, CCPA)

## Project Structure

- Keep route handlers in separate files when they grow beyond 50 lines
- Use middleware for cross-cutting concerns (logging, auth, validation)
- Store configuration in environment variables, not in code
- Follow the existing project structure and conventions

## Error Handling

- Always handle errors gracefully with try/catch blocks
- Return appropriate HTTP status codes (400 for client errors, 500 for server errors)
- Never expose internal error details to clients in production
- Log errors with sufficient context for debugging
