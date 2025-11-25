# Contributing to MailO

First off, thank you for considering contributing to MailO! It's people like you that make MailO such a great tool.

## Code of Conduct

This project and everyone participating in it is governed by our Code of Conduct. By participating, you are expected to uphold this code.

## How Can I Contribute?

### Reporting Bugs

Before creating bug reports, please check the existing issues to avoid duplicates. When you create a bug report, include as many details as possible:

- **Use a clear and descriptive title**
- **Describe the exact steps to reproduce the problem**
- **Provide specific examples**
- **Describe the behavior you observed and what you expected**
- **Include screenshots if possible**
- **Include your environment details** (OS, Node version, Docker version, etc.)

### Suggesting Enhancements

Enhancement suggestions are tracked as GitHub issues. When creating an enhancement suggestion, include:

- **Use a clear and descriptive title**
- **Provide a detailed description of the suggested enhancement**
- **Explain why this enhancement would be useful**
- **List any similar features in other applications**

### Pull Requests

1. Fork the repository
2. Create a new branch (`git checkout -b feature/amazing-feature`)
3. Make your changes
4. Commit your changes (`git commit -m 'Add some amazing feature'`)
5. Push to the branch (`git push origin feature/amazing-feature`)
6. Open a Pull Request

#### Pull Request Guidelines

- Follow the existing code style
- Write clear, descriptive commit messages
- Include tests for new features
- Update documentation as needed
- Ensure all tests pass
- Keep pull requests focused on a single feature/fix

## Development Setup

```bash
# Clone your fork
git clone https://github.com/YOUR_USERNAME/mailo.git
cd mailo

# Add upstream remote
git remote add upstream https://github.com/limitlessinfotechsolution/mailo.git

# Install dependencies
npm install

# Create a feature branch
git checkout -b feature/my-feature

# Make your changes...

# Run tests
npm test

# Commit and push
git commit -m "feat: add my feature"
git push origin feature/my-feature
```

## Commit Message Convention

We follow the [Conventional Commits](https://www.conventionalcommits.org/) specification:

```
type(scope): subject

body

footer
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, etc.)
- `refactor`: Code refactoring
- `test`: Adding or updating tests
- `chore`: Maintenance tasks
- `perf`: Performance improvements

### Examples

```
feat(calendar): add recurring events support

Implemented weekly, monthly, and yearly recurrence patterns
for calendar events with customizable end dates.

Closes #123
```

```
fix(auth): resolve JWT token expiration issue

Fixed a bug where JWT tokens were expiring prematurely
due to incorrect timezone handling.

Fixes #456
```

## Code Style

### JavaScript/React

- Use ES6+ features
- Use functional components with hooks
- Use async/await for asynchronous operations
- Follow ESLint rules
- Use meaningful variable names
- Add comments for complex logic

### File Naming

- Components: `PascalCase.jsx`
- Utilities: `camelCase.js`
- Constants: `UPPER_SNAKE_CASE.js`

### Code Example

```javascript
import { useState, useEffect } from 'react';
import { fetchData } from './api';

/**
 * Component description
 * @param {Object} props - Component props
 */
function MyComponent({ userId }) {
  const [data, setData] = useState(null);
  const [loading, setLoading] = useState(true);

  useEffect(() => {
    loadData();
  }, [userId]);

  const loadData = async () => {
    try {
      setLoading(true);
      const result = await fetchData(userId);
      setData(result);
    } catch (error) {
      console.error('Failed to load data:', error);
    } finally {
      setLoading(false);
    }
  };

  if (loading) return <div>Loading...</div>;
  
  return <div>{data?.name}</div>;
}

export default MyComponent;
```

## Testing

- Write unit tests for new features
- Ensure all tests pass before submitting PR
- Aim for high test coverage
- Test edge cases

```bash
# Run tests
npm test

# Run tests with coverage
npm run test:coverage

# Run specific test
npm test -- MyComponent.test.js
```

## Documentation

- Update README.md if needed
- Add JSDoc comments for functions
- Update API documentation for new endpoints
- Include examples in documentation

## Review Process

1. Automated checks must pass (CI/CD)
2. Code review by maintainers
3. Address review feedback
4. Approval and merge

## Community

- Be respectful and constructive
- Help others in discussions
- Share knowledge and experiences
- Follow the Code of Conduct

## Questions?

Feel free to ask questions by:
- Opening a GitHub Discussion
- Commenting on relevant issues
- Contacting maintainers

## License

By contributing, you agree that your contributions will be licensed under the MIT License.

---

**Thank you for contributing to MailO!**

*Limitless Infotech Solution Pvt Ltd.*
