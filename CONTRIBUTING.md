# Contributing to Blend DSL

We are excited that you are interested in contributing to Blend DSL! Contributions are welcome in various forms, such as reporting issues, suggesting new features, improving documentation, or submitting code changes.

## How to Contribute

### 1. Fork the Repository
To contribute, start by forking the repository to your own GitHub account:

1. Navigate to the [Blend DSL repository](https://github.com/your-username/blend-dsl).
2. Click on the "Fork" button in the top-right corner.
3. This will create a copy of the repository in your GitHub account.

### 2. Clone Your Fork
Clone the forked repository to your local machine:

```bash
git clone https://github.com/your-username/blend-dsl.git
cd blend-dsl
```

### 3. Create a New Branch
Always create a new branch to work on your changes. The branch name should reflect the feature or bug you're working on.

```bash
git checkout -b feature/new-feature-name
```

### 4. Make Your Changes
Work on your changes in the new branch. For larger changes, please ensure that your code is well-commented and follows the style of the existing codebase.

### 5. Commit Your Changes
After making your changes, commit them with a clear and concise commit message:

```bash
git add .
git commit -m "Add a brief description of the changes"
```

### 6. Push to Your Fork
Push your changes to the new branch in your forked repository:

```bash
git push origin feature/new-feature-name
```

### 7. Open a Pull Request (PR)
Once your changes are ready for review, open a pull request to merge your branch into the `main` branch of the original repository:

1. Go to your forked repository on GitHub.
2. Click the "Compare & pull request" button next to your new branch.
3. Provide a detailed description of your changes in the PR and submit it for review.

The project maintainers will review your pull request, and if necessary, request additional changes.

## Code Guidelines

Please ensure that your code adheres to the following guidelines:

- **Code Style**: Follow the existing code style used in the repository. Use tools like ESLint to ensure code quality.
- **Tests**: Include unit or integration tests for any new features or bug fixes.
- **Commit Messages**: Use clear, descriptive commit messages.

## Bug Reports and Feature Requests

If you find a bug or have an idea for a new feature, please [open an issue](https://github.com/your-username/blend-dsl/issues) in the repository. Make sure to provide enough details, including steps to reproduce the bug (if applicable) and any relevant context.

## Reporting Issues

To report an issue:

1. Navigate to the [issues page](https://github.com/your-username/blend-dsl/issues).
2. Click on "New Issue".
3. Select "Bug Report" or "Feature Request" depending on the nature of your issue.
4. Provide a clear and detailed description of the problem or suggestion.

## Running Tests

If you modify code or add new features, please ensure that the existing tests still pass, and add tests for new functionality.

1. Install dependencies if you haven't already:

   ```bash
   npm install
   ```

2. Run the tests:

   ```bash
   npm test
   ```

Make sure all tests pass before submitting your changes.

