# Contributing to PyScape

Thank you for your interest in contributing to PyScape! This guide will help you get started.

---

## 🤝 Code of Conduct

Be respectful, inclusive, and constructive. No harassment or discrimination of any kind.

---

## 🚀 Quick Start

### 1. Fork & Clone

```bash
# Fork the repo on GitHub, then:
git clone https://github.com/YOUR-USERNAME/pyscape-multi-generation.git
cd pyscape-multi-generation
```

### 2. Create a Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/your-bug-fix
```

### 3. Set Up Development Environment

```bash
npm install
# (See docs/GETTING_STARTED.md for detailed setup)
```

### 4. Make Changes

- Write code following the style guide below
- Add/update tests
- Update documentation
- Keep commits atomic and descriptive

### 5. Test Your Changes

```bash
npm test
npm run build
```

### 6. Commit & Push

```bash
git commit -m "feat: add amazing feature"
git push origin feature/your-feature-name
```

### 7. Open Pull Request

- Clear description of changes
- Reference any related issues (#123)
- Screenshot of UI changes
- Link to documentation

---

## 📝 Commit Message Convention

Follow Conventional Commits:

```
type(scope): description

feat:       new feature
fix:        bug fix
docs:       documentation
style:      formatting
refactor:   code reorganization
perf:       performance improvement
test:       tests
chore:      maintenance
```

**Examples:**
```
feat(sandbox): add C++ code execution support
fix(duels): prevent duplicate submissions
docs(readme): update API reference
```

---

## 🎨 Code Style

### JavaScript/React

```javascript
// Use ES6+ syntax
const handleClick = () => {
  // ...
};

// Use functional components
const MyComponent = ({ prop1, prop2 }) => {
  return <div>{prop1}</div>;
};

// Use meaningful variable names
const userMasteryScore = 0.87;
```

### Formatting

```bash
# Format code (if using Prettier)
npm run format

# Lint code
npm run lint
```

### Comments

```javascript
// ✅ DO: Explain WHY, not WHAT
// Users need time to process feedback, so we debounce input
const debouncedSearch = useMemo(() => debounce(search, 300), [search]);

// ❌ DON'T: State the obvious
// Set debouncedSearch to debounced search function
```

---

## 🧪 Testing

### Write Tests

```javascript
// For new features, add tests
describe('getUserSkills', () => {
  it('returns unlocked skills', async () => {
    const skills = await getUserSkills(userId);
    expect(skills).toContain(expect.objectContaining({
      status: 'eligible'
    }));
  });
});
```

### Run Tests

```bash
npm test
npm test -- --coverage  # See code coverage
```

### Coverage Targets

- **Statements**: > 70%
- **Branches**: > 60%
- **Functions**: > 70%
- **Lines**: > 70%

---

## 📚 Documentation

### Update Docs When:

- Adding features → Add to feature guide
- Changing API → Update API reference
- Fixing bugs → Update troubleshooting if relevant
- Changing database → Update schema docs

### Documentation Style

```markdown
# Feature Title

Brief description (1-2 sentences)

## Overview
More detailed explanation

## How It Works
Step-by-step explanation with examples

## API Reference
List of functions/endpoints

## Examples
Code examples

## Related
Links to related docs
```

---

## 🔄 Pull Request Process

### Before Opening PR

- [ ] Tests pass locally
- [ ] Code formatted and linted
- [ ] Documentation updated
- [ ] No unrelated changes

### PR Description Template

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation

## How to Test
Steps to verify changes work

## Screenshots (if UI change)
Images showing before/after

## Checklist
- [ ] Tests added/updated
- [ ] Docs updated
- [ ] No breaking changes
```

### Review Process

- At least 1 review required
- Address feedback promptly
- Keep PR focused and atomic
- Squash commits before merge (if requested)

---

## 🐛 Reporting Issues

### Bug Report Template

```markdown
## Describe the Bug
Clear description of what went wrong

## Steps to Reproduce
1. Click on...
2. See error...

## Expected Behavior
What should happen instead

## Screenshots
Include screenshots if helpful

## Environment
- OS: Windows/Mac/Linux
- Browser: Chrome/Firefox
- Node version: v16.x
```

### Feature Request

```markdown
## Feature Description
What feature would be useful?

## Use Case
Why is this needed?

## Proposed Solution
How should it work?

## Alternatives
Any other approaches?
```

---

## 📂 Project Structure

```
pyscape-multi-generation/
├── src/
│   ├── components/      # React components
│   ├── pages/          # Page-level components
│   ├── services/       # API & business logic
│   ├── context/        # State management
│   └── utils/          # Helper functions
├── backend/            # Node.js backend
├── migrations/         # Database migrations
├── scripts/            # Utility scripts
├── docs/               # Documentation
└── tests/              # Test files
```

### Adding a New Feature

1. Create component in `src/components/FeatureName/`
2. Add service in `src/services/`
3. Add tests in `tests/`
4. Add documentation in `docs/features/`
5. Update main `README.md`

---

## 🚀 Areas for Contribution

### Code

- Bug fixes ([Issues](https://github.com/yourusername/pyscape-multi-generation/issues))
- Performance improvements
- Test coverage
- Accessibility (a11y)
- Browser compatibility

### Documentation

- Improve clarity
- Add examples
- Update outdated sections
- Translate docs (i18n)

### Content

- Add more problems for duels
- Create tutorial videos
- Write blog posts
- Create course content

### Design

- UI/UX improvements
- Accessibility enhancements
- Animation refinements
- Mobile optimization

---

## 💬 Communication

### Getting Help

- 📖 [Documentation](../docs/)
- 💬 [Discussions](https://github.com/yourusername/pyscape-multi-generation/discussions)
- 🐛 [Issues](https://github.com/yourusername/pyscape-multi-generation/issues)

### Contact Maintainers

- Create an issue for design decisions
- Start a discussion for ideas
- Comment on PRs for feedback

---

## 🏆 Contributor Recognition

Contributors are recognized in:
- `CONTRIBUTORS.md` file
- README.md "Thanks to" section
- Release notes
- PyScape community channels

---

## 📜 License

By contributing, you agree your code is licensed under the MIT License.

---

## 🎓 Resources

- [React Documentation](https://react.dev)
- [Node.js Best Practices](https://nodejs.org/en/docs/)
- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Conventional Commits](https://www.conventionalcommits.org/)

---

**Happy contributing! 🚀**

Last updated: May 27, 2026
