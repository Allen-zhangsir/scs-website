# SCS Website SCF Deployment Payload

This file is the canonical CloudQ handoff for deploying the SCS official website to Tencent Cloud SCF.

## Target

- Region: `ap-guangzhou`
- Namespace: `default`
- FunctionName: `scs-website`
- Runtime: `Nodejs18.15`
- Handler: `index.main_handler`
- MemorySize: `128`
- Timeout: `3`

Do not modify `scs-workbuddy-oauth`.

## Verified deployment payload

The original ZIP is represented as four contiguous Base64 text chunks. Fetch all four raw files in this exact order and concatenate the response bodies with **no delimiter, no whitespace, no newline inserted between parts**.

1. https://raw.githubusercontent.com/Allen-zhangsir/scs-website/main/deployment/base64/SCS_Website_SCF_Node18_Deploy.zip.b64.part1
2. https://raw.githubusercontent.com/Allen-zhangsir/scs-website/main/deployment/base64/SCS_Website_SCF_Node18_Deploy.zip.b64.part2
3. https://raw.githubusercontent.com/Allen-zhangsir/scs-website/main/deployment/base64/SCS_Website_SCF_Node18_Deploy.zip.b64.part3
4. https://raw.githubusercontent.com/Allen-zhangsir/scs-website/main/deployment/base64/SCS_Website_SCF_Node18_Deploy.zip.b64.part4

Verification metadata:

- Part 1 bytes: `6000`
- Part 2 bytes: `6000`
- Part 3 bytes: `6000`
- Part 4 bytes: `6140`
- Concatenated Base64 length: `24140`
- Decoded ZIP size: `18104` bytes
- Decoded ZIP SHA-256: `65598df8c712bcbe0cb5981f6c120a4cca4f87e6106c458c4557abe7c059b776`

The Git blob SHAs of all four parts were independently checked against the locally generated source payload before publication.

## CloudQ execution rule

Do **not** ask the user to resend the ZIP and do **not** require a local temporary ZIP file.

Fetch the four raw text chunks, concatenate them in memory, and submit the resulting complete Base64 string directly as Tencent SCF `Code.ZipFile`.

If you choose to decode the Base64 for integrity checking first, the resulting ZIP must be exactly `18104` bytes and its SHA-256 must equal:

`65598df8c712bcbe0cb5981f6c120a4cca4f87e6106c458c4557abe7c059b776`

Then execute `scf-CreateFunction` for `scs-website`.

After creation, poll `scf-GetFunction` until `Status = Active` before creating any trigger.

Only after `Status = Active`, create HTTP trigger `scs-website-url` with public anonymous extranet access, then validate:

- `/`
- `/en/`
- `/cases/insurance-ai`
- `/en/cases/insurance-ai`
- `/robots.txt`
- `/sitemap.xml`
- `/this-route-should-404`

Expected: first six HTTP 200, final route HTTP 404.

Do not proceed to ICP, SSL, DNS, or custom domain work until Preview passes.
