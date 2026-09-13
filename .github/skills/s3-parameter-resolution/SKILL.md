---
name: s3-parameter-resolution
description: 'Resolve and validate numbered AWS S3 bucket parameters from inputs/input.txt. Use when interpreting bucket names, regions, security settings, encryption, versioning, logging, Object Lock, lifecycle rules, or semicolon-separated tags.'
argument-hint: 'Resolve the S3 bucket parameters'
user-invocable: true
---

# S3 Parameter Resolution

Resolve the project S3 input file into a validated configuration. This skill owns parameter parsing and validation; it does not create buckets or execute AWS commands.

## Resources

- Read [instructions.md](../../instructions.md) for the authoritative S3 policy.
- Read [input.txt](../../inputs/input.txt) for the current parameter values.

## Procedure

1. Read each numbered parameter and the metadata line immediately below it.
2. Extract the value between quotes after `=`.
3. If the value is empty, apply its declared `default` when one exists. Keep required fields unresolved when they have no default.
4. Validate `Bucket_name` and `AWS_region` as required fields.
5. Validate boolean and enumerated values against the choices shown in the input metadata.
6. Apply conditional validation:
   - `SSE-KMS` requires `KMS_key_id`.
   - Access logging requires `Logging_target_bucket`.
   - Object Lock requires `Object_lock_mode` and `Object_lock_retention_days`.
7. Parse `Tags` as semicolon-separated `key=value` pairs. Reject malformed pairs and more than 50 tags.
8. Return a resolved configuration, validation errors, and warnings. Do not execute commands or expose credentials.

## Output

Return these sections:

- `Resolved values`
- `Validation errors`
- `Warnings`
- `Conditional settings`

If all required values are valid, state that the configuration is ready for a separate execution workflow.
