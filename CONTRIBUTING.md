# Contributing to OpenCOOS

Thank you for helping build **COOS, the Common Ownership Operating Schema**, an open data model for strata and condominium communities across Canada.

This guide applies to every repository in the [OpenCOOS organization](https://github.com/opencoos) unless a repository has its own.

**You don't need to be a developer.** The most valuable contributions are often a council member, board director, property manager or professional saying, "That's not how it works in our building" or "In Ontario we call that something else."

## Contents

- [Ground rules](#ground-rules)
- [Ways to contribute](#ways-to-contribute)
- [Where to contribute](#where-to-contribute)
- [Proposing changes to the specification](#proposing-changes-to-the-specification)
- [Working on the specification](#working-on-the-specification)
- [Working on the website](#working-on-the-website)
- [Commits and sign-off (DCO)](#commits-and-sign-off-dco)
- [Review and decisions](#review-and-decisions)
- [Licence](#licence)

## Ground rules

- **Never share real personal or confidential information.** Use fictional examples. Do not post owner names, contact details, unit numbers tied to real people, financial records, legal documents or anything else private to a strata or condominium corporation.
- **Disclose your affiliation.** If you work for a software vendor, property management company or other organization with an interest in a change, say so when you propose it. Affiliations are welcome; undisclosed ones aren't.
- **Describe the real-world problem first.** A proposed solution is optional. A clear example of how things work today is often more useful.
- **Be respectful.** Assume good intent, keep discussion about the work, and remember that contributors come from different provinces, professions and levels of technical experience.
- **This is not legal advice.** Discussions about terminology are about modelling data, not interpreting legislation.

## Ways to contribute

| If you are… | You can… |
| --- | --- |
| A strata council member, condo board director or owner | Check that definitions match how your council or board actually works; tell us which records are hardest to find or move |
| A property manager | Tell us which exports and integrations cost the most time; review definitions against day-to-day workflows |
| A lawyer, accountant, engineer, insurer or appraiser | Review terminology in your area and province; flag text that could be misread as legal guidance |
| A software vendor | Map your data model to COOS and report what didn't fit; tell us about planned implementations |
| A developer | Improve schemas, examples, validation and documentation |
| A researcher | Identify data needed to study strata and condo housing; advise on privacy-preserving structures |

## Where to contribute

| Repository | Use it for |
| --- | --- |
| [opencoos/spec](https://github.com/opencoos/spec) | Anything about the data model: entities, fields, vocabularies, terminology, provinces, examples, versioning |
| [opencoos/website](https://github.com/opencoos/website) | The documentation site: errors, broken links, accessibility, layout |
| [opencoos/.github](https://github.com/opencoos/.github) | This guide, the issue templates and the organization profile |

For questions, ideas and early conversations, use [Discussions](https://github.com/opencoos/spec/discussions). It's a good place to start if you're not sure whether something is an issue. For a specific problem or change, open an issue and choose a template; if none fits, a plain issue is fine.

## Proposing changes to the specification

The process depends on the size of the change.

**Small changes** — typos, clearer descriptions, fixed examples, documentation: open a pull request directly.

**Substantial changes** — a new entity or domain, a new field, a change to a controlled vocabulary, anything breaking, or support for a new province:

1. **Open a proposal issue** in [opencoos/spec](https://github.com/opencoos/spec/issues/new/choose) using the *Proposal* template. Describe the problem, real-world (fictional) examples, the proposed definitions, which provinces it affects, and alternatives you considered.
2. **Discussion.** The proposal stays open for comment for a reasonable period, normally at least two weeks for anything breaking, so people from different provinces and roles can respond.
3. **Decision.** Maintainers aim for consensus, guided by the design principles and real-world evidence. The decision and its reasoning are recorded on the issue.
4. **Pull request.** Once accepted, the change is made by pull request (by you or a maintainer) and lands in the next draft or release.

While COOS is below 1.0.0, any release may contain breaking changes, but they are always listed in the changelog with migration notes. See the [versioning policy](https://github.com/opencoos/website/blob/main/app/docs/versioning/page.mdx).

## Working on the specification

The specification lives in [opencoos/spec](https://github.com/opencoos/spec):

```
spec.json              Name, version, status, domains, schema ID prefix
changelog.json         Releases and open proposals
domains/*.json         Purpose, scope, planned entities, open issues
schemas/
  common.schema.json   Shared definitions (Identifier, Money, Address, …)
  <domain>/<Entity>.schema.json
examples/<Entity>.example.json
```

When you change the specification:

- **Follow the conventions.** Entities are PascalCase, fields and vocabulary values are lowerCamelCase, reference fields end in `Id`/`Ids`, money is a decimal string with a currency, and dates are ISO 8601. See [conventions and naming](https://github.com/opencoos/website/blob/main/app/docs/conventions/page.mdx).
- **Keep every entity's example valid**, using fictional data only.
- **Set the status honestly.** New entities start as `experimental` or `proposed`; nothing becomes `stable` outside a release.
- **Flag legal terminology** that needs review in `x-legalReviewNotes`.
- **Record the change** in `changelog.json` under the current draft.

### Validating your change

Validation runs from the website repository, which includes the specification as a git submodule:

```bash
git clone --recurse-submodules https://github.com/opencoos/website.git
cd website
npm install

# Point the site at your local copy of the spec
SPEC_DIR=../path/to/your/spec npm run spec:validate

# Optionally, preview the documentation with your changes
SPEC_DIR=../path/to/your/spec npm run dev
```

`spec:validate` compiles every schema, validates every example against its schema, and checks that relationships point to real entities. Pull requests should pass it.

## Working on the website

```bash
git clone --recurse-submodules https://github.com/opencoos/website.git
cd website
npm install
npm run dev        # http://localhost:3000
```

Before opening a pull request:

```bash
npm run lint
npm run typecheck
npm run build      # also validates the specification
```

The site is Next.js (App Router), TypeScript, Tailwind CSS and shadcn/ui, with documentation in MDX under `app/docs`. Keep pages accessible (semantic headings, keyboard navigation, sufficient contrast) and never present draft definitions as final, invent endorsements or statistics, or claim tooling exists before it does.

## Commits and sign-off (DCO)

OpenCOOS uses the [Developer Certificate of Origin](https://developercertificate.org/) (DCO) instead of a contributor licence agreement. You keep the copyright in your contribution; signing off certifies that you wrote it, or otherwise have the right to submit it under the project's licence.

Add a sign-off line to every commit with `-s`:

```bash
git commit -s -m "Clarify unit entitlement description"
```

This appends a line using your Git name and email:

```
Signed-off-by: Alex Example <alex@example.com>
```

If you forgot, amend the last commit with `git commit --amend -s --no-edit`, or sign off a whole branch with `git rebase --signoff main`.

## Review and decisions

- Maintainers review pull requests and aim to respond within a week.
- Changes to the specification need approval from at least one maintainer. Substantial changes also need an accepted proposal.
- Maintainers act in the interest of the standard, not of any one product — including products they work on — and disclose their own affiliations.
- During early development, maintainers are drawn from the ManageStrata team, which founded OpenCOOS. The goal is to add maintainers from independent organizations as the community grows. See [governance](https://github.com/opencoos/website/blob/main/app/governance/page.tsx).

## Licence

All OpenCOOS repositories are licensed under the [Apache License, Version 2.0](LICENSE). By contributing, you agree that your contributions are licensed under the same terms. The Apache License does not grant rights to the names "COOS" or "OpenCOOS" or the OpenCOOS logo.
