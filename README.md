# Secure AI Development Advanced (201) Workshop

In this workshop, you use AI coding agents in Cursor to add features to a small Express app. You also learn how to keep the generated code secure.

**Time:** 30 minutes
**Level:** Intermediate. You must finish the Secure AI Development Foundations (101) workshop first.

## What you will learn

1. **AGENTS.md:** How to use an `AGENTS.md` file to give coding agents your rules for code quality, security, and compliance.
2. **Cloud Agents:** When to use Cursor Cloud Agents and when to use local agents. You also learn the security risks of each.
3. **Best-of-N:** How to run one prompt on several AI models at the same time, and then pick the best result.

## Prerequisites

- [Cursor](https://cursor.com) installed
- The Snyk extension installed in Cursor
- [Node.js](https://nodejs.org) 18 or later, with npm
- The 101 workshop finished

## Setup

1. Clone the repository and open the folder:

   ```bash
   git clone https://github.com/snyk-labs/sko2026-secure-ai-dev-advanced-workshop.git
   cd sko2026-secure-ai-dev-advanced-workshop
   ```

2. Install the dependencies:

   ```bash
   npm install
   ```

3. Start the server:

   ```bash
   npm start
   ```

4. Open [http://localhost:3000](http://localhost:3000). You see a "Hello, World!" page.

5. Open [http://localhost:3000/api/health](http://localhost:3000/api/health). You see a JSON response with `"status": "ok"`.

To use a different port, set the `PORT` variable, for example `PORT=3001 npm start`.

To restart the server automatically when files change, run `npm run dev`.

The app has one API route, `GET /api/health`. The files in `src/public` are served as static files. The exercises below add more routes in `src/index.js`.

## Section 1: AGENTS.md

`AGENTS.md` is a Markdown file in the root of a project. It contains instructions for AI coding agents. Agents such as Cursor read it and follow it. Many other tools also support it. Because it is a plain file, you can keep it in version control with your code.

Open `AGENTS.md` in this project. It has these sections:

- **Code Quality Standards:** JSDoc comments, `async`/`await`, input validation, unit tests
- **Security Guidelines:** no logging of sensitive data, parameterized queries, password hashing
- **Compliance Guidelines:** no GPL-licensed dependencies
- **Project Structure** and **Error Handling**

### Exercise 1: See AGENTS.md in action

1. Open the Cursor agent and enter this prompt:

   ```text
   Add a user registration endpoint at POST /api/register that accepts email and password, validates the input, and returns a user object with an ID
   ```

2. Look at the code that the agent writes. Check for these items:
   - JSDoc comments on the functions
   - Validation of the input
   - No logging of the password
   - `async`/`await` instead of `.then()`

3. Enter a second prompt:

   ```text
   Add a password reset endpoint at POST /api/reset-password that accepts an email address, validates it, and returns a success message
   ```

4. Check the new code against the same list.

## Section 2: Cloud Agents and security

Cursor has two kinds of agents:

| Agent | Where it runs | Notes |
|-------|---------------|-------|
| Main agent and local subagents | Your computer | Can use your extensions (such as Snyk), `AGENTS.md`, and local MCP servers |
| Cloud Agents | A virtual machine in Cursor's cloud | Cannot use your local extensions or local MCP servers. Might not follow `AGENTS.md` (known issue) |

Use a local agent when:

- You want real-time Snyk scans in the IDE.
- You need `AGENTS.md` to be followed.
- You work in an interactive session.

Use a Cloud Agent when:

- The task takes a long time (30 minutes or more).
- You want to close your laptop while the agent works.
- The task runs many tests.
- Your pull requests are scanned by Snyk in your pipeline.

**Risk:** A Cloud Agent has no access to your Snyk extension. The code it writes is not scanned in your IDE.

To reduce this risk, add scans after the agent finishes:

1. **Pull request scans:** Connect Snyk to your GitHub or GitLab pull request checks.
2. **CI pipeline:** Run `snyk code test` and `snyk test` in CI.
3. **Bugbot:** Use Cursor's Bugbot to review pull requests automatically.

## Section 3: Best-of-N

Best-of-N runs the same prompt on several models at the same time. Each model works in its own git worktree. You compare the results and apply the one you like best.

### Exercise 2: Try Best-of-N

1. Write this prompt in the agent input. Do not send it yet.

   ```text
   Create a rate limiting middleware that limits requests to 100 per minute per IP address
   ```

2. Click the **1x** button next to the model selector.
3. Select **Multiple models**.
4. Choose two or three models from different providers.
5. Send the prompt.
6. Compare the results side by side. Ask yourself:
   - Which code is easiest to read?
   - Which code handles edge cases best?
   - Which code would you use in production?
7. Click **Apply** on the best result.

Best-of-N helps most with hard problems and security-critical code. Different models take different approaches and find different issues.

## Key takeaways

- `AGENTS.md` gives every agent and every team member the same rules.
- Cloud Agents skip your IDE checks. Always scan pull requests with Snyk.
- Best-of-N lets you compare several answers before you choose one.

## Troubleshooting

**The server does not start**

1. Make sure you are in the project folder.
2. Reinstall the dependencies:

   ```bash
   rm -rf node_modules
   npm install
   ```

3. Start the server again with `npm start`.

If the port is already in use, start the server on another port, for example `PORT=3001 npm start`.

**The agent does not follow AGENTS.md**

- Make sure the file is named `AGENTS.md` (uppercase) and is in the project root.
- Start a new agent session.
- Use a local agent. Cloud Agents might not read the file.

**The Snyk extension does not scan**

1. Open the Extensions panel (Cmd/Ctrl+Shift+X).
2. Search for "Snyk" and make sure it is installed.
3. Press Cmd/Ctrl+Shift+P and run **Snyk: Authenticate**.

**Best-of-N shows only one option**

- Make sure you clicked **1x** and selected **Multiple models**.
- Some models need a specific Cursor plan.

## More information

- [Cursor documentation](https://cursor.com/docs)
- [AGENTS.md specification](https://agents.md/)
- [Snyk documentation](https://docs.snyk.io)
