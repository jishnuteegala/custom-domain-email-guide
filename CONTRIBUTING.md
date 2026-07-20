# Contributing to Custom Domain Email Guide

First off, thank you for considering contributing! This guide aims to help as many people as possible get professional email on their own domain, and your input is valuable.

## How Can I Contribute?

### 🐛 Reporting Issues

If you find an error, unclear instruction, or missing information:

1. Check if the issue already exists
2. Open a new issue with:
   - Clear description of the problem
   - Steps to reproduce (if applicable)
   - Your email provider (Gmail/Outlook/etc.) and DNS provider
   - Screenshots of error messages (redact personal addresses!)

### 💡 Suggesting Enhancements

Have an idea to improve the guide?

- Open an issue describing your suggestion
- Explain why it would be helpful
- Provide examples if possible

### 📝 Pull Requests

Ready to contribute directly?

1. **Fork** the repository
2. **Create a branch**: `git checkout -b feature/your-improvement`
3. **Make your changes**:
   - Keep language clear and beginner-friendly
   - Test instructions if possible
   - Update table of contents if adding sections
4. **Commit** using the guidelines below.
5. **Push**: `git push origin feature/your-improvement`
6. **Open a Pull Request** with a clear description

### 📋 Style Guidelines

- Use clear, concise language
- Include exact field values in tables where forms are involved
- Add examples for complex concepts
- Keep formatting consistent with existing content
- Test steps before submitting
- Never include real email addresses, app passwords, or domain-specific secrets in examples

### 📝 Commit Message Guidelines

Use a concise, Conventional Commits–style format tailored for this docs-only guide:

- `docs(scope):` content changes to the guide (preferred for new sections)
- `fix(scope):` correct wrong values/steps or inaccurate statements
- `style(scope):` formatting-only tweaks (spacing, punctuation, Markdown)
- `refactor(scope):` restructure sections/anchors without changing meaning
- `chore(scope):` repo maintenance (links, badges, metadata), changelog updates
- `release:` version bumps and tagging alongside changelog entries

**Notes:**
- Use a clear `scope` like `receiving`, `sending`, `troubleshooting`, or `faq`.
- Avoid `feat:` for documentation additions; use `docs:` instead. Reserve `feat:` only if adding tooling/automation.
- If renaming anchors/sections (breaking deep links), include `BREAKING CHANGE:` in the footer and bump the major version per the changelog rules.

**Examples:**
- `docs(sending): add Outlook connected-accounts alternative`
- `fix(reference): correct SMTP port for SSL variant`
- `style(readme): normalize fenced bash blocks`
- `refactor(toc): reorder sections, preserve anchors`
- `chore(changelog): set v1.0 dated 2026-07-20`
- `release: v1.0`

### 🌍 Translations

Want to translate the guide to another language?

1. Create a new file: `README.[language-code].md` (e.g., `README.es.md` for Spanish)
2. Translate all content while maintaining formatting
3. Update the main README to link to your translation
4. Submit as a Pull Request

### ✅ Good First Contributions

New to contributing? Start here:

- Fix typos or grammatical errors
- Improve unclear explanations
- Add missing troubleshooting scenarios
- Update outdated links or dashboard paths (Cloudflare's UI moves around!)
- Add provider-specific tips you've discovered

## Code of Conduct

### Our Pledge

We are committed to providing a welcoming and inclusive environment for everyone, regardless of:
- Experience level
- Gender identity and expression
- Sexual orientation
- Disability
- Personal appearance
- Body size
- Race, ethnicity, or nationality
- Age
- Religion

### Expected Behavior

- Be respectful and constructive
- Welcome newcomers warmly
- Accept feedback gracefully
- Focus on what's best for the community

### Unacceptable Behavior

- Harassment, trolling, or insulting comments
- Personal attacks
- Publishing others' private information
- Other conduct inappropriate in a professional setting

## Questions?

Don't hesitate to ask! Open an issue with your question or start a discussion.

## Recognition

Contributors will be acknowledged in releases and can add themselves to a CONTRIBUTORS.md file (create one if it doesn't exist).

---

Thank you for helping make custom domain email accessible to everyone! 🙏
