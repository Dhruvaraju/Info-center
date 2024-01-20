- [What is gerrit?](#what-is-gerrit)
  - [Why to use gerrit?](#why-to-use-gerrit)
  - [Code Review](#code-review)
    - [What does code review contains?](#what-does-code-review-contains)
  - [Basic Gerrit Terminology](#basic-gerrit-terminology)

## What is gerrit?

#gerrit
An opensource, source code management tool, which can manage multiple repositories, branches, tags and other git resources. It uses git for version control. It also provides code review and access control on git repos. Gerrit stores changes before they are pushed to repository branches.

### Why to use gerrit?

- Provides lightweight framework for reviewing code before they are accepted into repository.
- Captures discussion on reviews and code changes, which are persistent and auditable.
- Control team workflows to ensure all quality checks are met.
- Manage access control for repos and web ui.
- No additional tools required to interact.

### Code Review

- A commit is pushed as a change, which is kept in staging for review.
- This change can be reviewed, once review is approved it can be merged to repository.

#### What does code review contains?

- Comments
- Approvals or rejections
- Additional patches to fix issues
- Diff between versions
- Dependencies
- Change status

### Basic Gerrit Terminology

**Change:** A change represents a single commit that is under review. Each change has a unique change Id. #gerrit-change

**Pathset:** patchsets are subsequent commits that are attempts to amend an existing change. #gerrit-patchset
