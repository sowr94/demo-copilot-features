---
name: Preview S3 Bucket Command
description: "Generate a validated AWS CLI preview for creating an S3 bucket from inputs/input.txt without executing it."
argument-hint: "Preview the S3 bucket creation command"
agent: "agent"
tools: [read, search]
---

Read [instructions.md](../../instructions.md) and [inputs/input.txt](../../inputs/input.txt).

Resolve the parameter values according to the policy in `instructions.md`, then produce a dry-run preview only.

Include:

1. The resolved bucket name and AWS region.
2. The security, encryption, versioning, logging, Object Lock, lifecycle, and tag settings that will be applied.
3. Validation errors or warnings, including missing required values.
4. The AWS CLI commands that would create and configure the bucket.
5. A clear statement that no command was executed.

Do not execute AWS commands, request credentials, or include secret values. If required values are missing or invalid, show the issues and do not generate an executable creation command.
