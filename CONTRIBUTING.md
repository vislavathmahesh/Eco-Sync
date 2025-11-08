# EcoSync - Contributing Guidelines

Thank you for considering contributing to EcoSync! This document outlines the process and guidelines for contributing.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Testing Guidelines](#testing-guidelines)
- [Documentation](#documentation)

## 📜 Code of Conduct

### Our Pledge

We pledge to make participation in our project a harassment-free experience for everyone, regardless of age, body size, disability, ethnicity, gender identity and expression, level of experience, nationality, personal appearance, race, religion, or sexual identity and orientation.

### Our Standards

**Positive behavior includes:**
- Using welcoming and inclusive language
- Being respectful of differing viewpoints
- Gracefully accepting constructive criticism
- Focusing on what is best for the community
- Showing empathy towards other community members

**Unacceptable behavior includes:**
- Trolling, insulting/derogatory comments, and personal or political attacks
- Public or private harassment
- Publishing others' private information without explicit permission
- Other conduct which could reasonably be considered inappropriate

## 🚀 Getting Started

1. **Fork the repository**
   ```bash
   git clone https://github.com/yourusername/ecosync.git
   cd ecosync
   ```

2. **Set up development environment**
   - Follow the [Installation Guide](README.md#-installation) in README.md
   - Ensure all tests pass before making changes

3. **Find an issue to work on**
   - Check [Issues](https://github.com/yourusername/ecosync/issues) for `good-first-issue` or `help-wanted` labels
   - Comment on the issue to let others know you're working on it
   - If creating a new feature, open an issue first to discuss

## 🔄 Development Workflow

### 1. Create a Feature Branch

```bash
git checkout -b feature/your-feature-name
# or
git checkout -b fix/bug-description
```

**Branch naming conventions:**
- `feature/` - New features
- `fix/` - Bug fixes
- `docs/` - Documentation updates
- `refactor/` - Code refactoring
- `test/` - Adding tests
- `chore/` - Maintenance tasks

### 2. Make Your Changes

- Write clean, readable code
- Follow existing code style
- Add comments for complex logic
- Update documentation if needed

### 3. Test Your Changes

```bash
# Frontend
cd frontend
npm run lint
npm run build

# Backend
cd backend
python -m pytest  # (when tests are added)
```

### 4. Commit Your Changes

```bash
git add .
git commit -m "feat: add amazing feature"
```

See [Commit Guidelines](#commit-guidelines) below.

### 5. Push and Create Pull Request

```bash
git push origin feature/your-feature-name
```

Then open a PR on GitHub with a clear description.

## 📏 Coding Standards

### Frontend (JavaScript/React)

**Style Guide:**
- Use ESLint with default Vite config
- Prettier for formatting (2 spaces, single quotes)
- Functional components with hooks
- Use PropTypes or TypeScript for type checking

**Component Structure:**
```jsx
// Imports
import { useState, useEffect } from 'react'
import { Button } from '@/components/ui/button'

// Component
export default function MyComponent({ prop1, prop2 }) {
  // State
  const [state, setState] = useState(null)
  
  // Effects
  useEffect(() => {
    // Effect logic
  }, [])
  
  // Handlers
  const handleClick = () => {
    // Handler logic
  }
  
  // Render
  return (
    <div className="container">
      {/* JSX */}
    </div>
  )
}
```

**Naming Conventions:**
- Components: PascalCase (`MyComponent.jsx`)
- Files: camelCase (`myUtils.js`)
- CSS classes: kebab-case or Tailwind utilities
- Functions: camelCase (`handleSubmit`)
- Constants: UPPER_SNAKE_CASE (`API_URL`)

### Backend (Python/Flask)

**Style Guide:**
- Follow PEP 8
- Use Black formatter (line length: 88)
- Type hints for function parameters and returns
- Docstrings for all functions and classes

**Function Structure:**
```python
def my_function(param1: str, param2: int) -> dict:
    """
    Brief description of function.
    
    Args:
        param1: Description of param1
        param2: Description of param2
        
    Returns:
        Description of return value
        
    Raises:
        ValueError: When something goes wrong
    """
    # Function logic
    return result
```

**Naming Conventions:**
- Functions: snake_case (`get_user_data`)
- Classes: PascalCase (`UserManager`)
- Constants: UPPER_SNAKE_CASE (`MAX_UPLOAD_SIZE`)
- Private methods: `_private_method`

## 💬 Commit Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/) specification.

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation changes
- `style`: Code style changes (formatting, no logic change)
- `refactor`: Code refactoring
- `perf`: Performance improvements
- `test`: Adding or updating tests
- `chore`: Maintenance tasks, dependencies

### Examples

```bash
feat(complaints): add resolution photo upload for staff

- Added file upload component for staff
- Store URLs in resolution_media_urls array
- Display photos in admin and citizen views

Closes #123
```

```bash
fix(auth): resolve login redirect issue

Fixed bug where users were not redirected after successful login.

Fixes #456
```

```bash
docs(readme): update installation instructions

Added detailed steps for database setup and migration.
```

## 🔀 Pull Request Process

### Before Submitting

- [ ] Code follows project style guidelines
- [ ] All tests pass locally
- [ ] New code has appropriate test coverage
- [ ] Documentation is updated (if applicable)
- [ ] No merge conflicts with main branch
- [ ] Commit messages follow conventional commits

### PR Template

When creating a PR, please include:

```markdown
## Description
Brief description of changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Related Issues
Closes #123

## Screenshots (if applicable)
[Add screenshots here]

## Testing
- [ ] Tested locally
- [ ] Added/updated tests
- [ ] Manual testing performed

## Checklist
- [ ] Code follows style guidelines
- [ ] Self-review completed
- [ ] Documentation updated
- [ ] No new warnings
```

### Review Process

1. **Automated Checks**: CI/CD runs linting and tests
2. **Code Review**: Maintainer reviews code for quality and standards
3. **Feedback**: Address any requested changes
4. **Approval**: Once approved, maintainer will merge

### Merge Requirements

- At least 1 approval from maintainer
- All CI checks passing
- No merge conflicts
- Up-to-date with main branch

## 🧪 Testing Guidelines

### Frontend Testing (Future)

```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Watch mode
npm run test:watch
```

**Test Structure:**
```jsx
import { render, screen, fireEvent } from '@testing-library/react'
import MyComponent from './MyComponent'

describe('MyComponent', () => {
  it('should render correctly', () => {
    render(<MyComponent />)
    expect(screen.getByText('Hello')).toBeInTheDocument()
  })
  
  it('should handle click events', () => {
    const handleClick = jest.fn()
    render(<MyComponent onClick={handleClick} />)
    fireEvent.click(screen.getByRole('button'))
    expect(handleClick).toHaveBeenCalledTimes(1)
  })
})
```

### Backend Testing (Future)

```bash
# Run all tests
pytest

# Run with coverage
pytest --cov=app

# Run specific test file
pytest tests/test_complaints.py
```

**Test Structure:**
```python
import pytest
from app import create_app

@pytest.fixture
def client():
    app = create_app()
    app.config['TESTING'] = True
    with app.test_client() as client:
        yield client

def test_get_complaints(client):
    """Test GET /api/complaints endpoint"""
    response = client.get('/api/complaints')
    assert response.status_code == 200
    assert 'data' in response.json
```

## 📚 Documentation

### Code Documentation

**JSDoc for JavaScript:**
```javascript
/**
 * Fetches complaints from the API
 * @param {Object} filters - Filter parameters
 * @param {string} filters.status - Complaint status
 * @param {string} filters.category - Complaint category
 * @returns {Promise<Array>} Array of complaints
 */
async function fetchComplaints(filters) {
  // Implementation
}
```

**Docstrings for Python:**
```python
def get_complaints(user_id: str = None) -> dict:
    """
    Retrieve complaints from database.
    
    Args:
        user_id: Optional user ID to filter by
        
    Returns:
        Dictionary with success status and complaint data
        
    Example:
        >>> get_complaints(user_id="123")
        {'success': True, 'data': [...]}
    """
    pass
```

### Updating Documentation

When making changes that affect:
- **API**: Update `docs/API.md` and README.md API section
- **Features**: Update README.md features section
- **Setup**: Update installation instructions
- **Database**: Update `database/schema.md`

## 🎯 Areas for Contribution

### Good First Issues

- UI improvements and animations
- Adding unit tests
- Improving error handling
- Documentation updates
- Accessibility improvements

### Advanced Contributions

- Mobile app development (React Native)
- AI-powered categorization
- Performance optimizations
- Route optimization algorithms
- Integration with IoT sensors

## 🤝 Getting Help

- **Issues**: Search existing issues or create new ones
- **Discussions**: Use GitHub Discussions for questions
- **Email**: maheshvislavath45@gmail.com

## 🏆 Recognition

Contributors will be:
- Listed in `CONTRIBUTORS.md`
- Mentioned in release notes

---

**Thank you for contributing to EcoSync! Together, we're building a cleaner, greener future. 🌿**
