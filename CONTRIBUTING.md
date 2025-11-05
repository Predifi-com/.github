# Contributing to Predifi

Thank you for your interest in contributing to Predifi! We welcome contributions from the community.

## 📋 Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Setup](#development-setup)
- [How to Contribute](#how-to-contribute)
- [Pull Request Process](#pull-request-process)
- [Coding Standards](#coding-standards)
- [Testing Guidelines](#testing-guidelines)
- [Commit Message Guidelines](#commit-message-guidelines)
- [Community](#community)

## 🤝 Code of Conduct

By participating in this project, you agree to abide by our Code of Conduct. We are committed to providing a welcoming and inspiring community for all.

### Our Standards

- **Be respectful** - Treat everyone with respect and kindness
- **Be collaborative** - Work together towards common goals
- **Be inclusive** - Welcome diverse perspectives and experiences
- **Be professional** - Maintain high standards in all interactions

## 🚀 Getting Started

### Prerequisites

- Node.js 18+ and npm/pnpm
- Foundry (for smart contracts)
- MongoDB (local or Atlas)
- Redis (local or Cloud)
- Git

### Development Setup

1. **Clone the repository**
   ```bash
   git clone https://github.com/Predifi-com/predifi.git
   cd predifi
   ```

2. **Backend Setup**
   ```bash
   cd backend
   npm install
   cp .env.example .env
   # Edit .env with your configuration
   npm run dev
   ```

3. **Smart Contracts Setup**
   ```bash
   cd contracts
   forge install
   forge test
   ```

4. **Run Tests**
   ```bash
   # Backend tests
   cd backend
   npm test
   
   # Smart contract tests
   cd contracts
   forge test
   ```

## 💡 How to Contribute

### Reporting Bugs

If you find a bug, please create an issue with:
- **Clear title** - Summarize the issue
- **Description** - Detailed explanation of the bug
- **Steps to reproduce** - How to trigger the bug
- **Expected behavior** - What should happen
- **Actual behavior** - What actually happens
- **Environment** - OS, Node version, etc.
- **Screenshots** - If applicable

### Suggesting Features

We love feature suggestions! Please create an issue with:
- **Clear title** - Summarize the feature
- **Use case** - Why is this feature needed?
- **Proposed solution** - How should it work?
- **Alternatives** - Other approaches you considered
- **Additional context** - Any other relevant information

### Security Issues

⚠️ **DO NOT** create public issues for security vulnerabilities!

If you discover a security issue, please email us at **admin@predifi.com** with:
- Description of the vulnerability
- Steps to reproduce
- Potential impact
- Suggested fix (if any)

We'll respond within 48 hours and work with you to resolve the issue.

## 🔄 Pull Request Process

### 1. Fork and Branch

```bash
# Fork the repository on GitHub
# Clone your fork
git clone https://github.com/YOUR_USERNAME/predifi.git
cd predifi

# Create a feature branch
git checkout -b feature/your-feature-name
# or
git checkout -b fix/your-bug-fix
```

### 2. Make Changes

- Write clean, readable code
- Follow our coding standards
- Add tests for new features
- Update documentation as needed
- Keep commits atomic and focused

### 3. Test Your Changes

```bash
# Run all tests
npm test

# Run specific tests
npm test -- src/tests/your-test.test.ts

# Check test coverage
npm run test:coverage

# Lint your code
npm run lint

# Format your code
npm run format
```

### 4. Commit Your Changes

Follow our [commit message guidelines](#commit-message-guidelines):

```bash
git add .
git commit -m "feat: add new feature"
git push origin feature/your-feature-name
```

### 5. Create Pull Request

- Go to the original repository on GitHub
- Click "New Pull Request"
- Select your branch
- Fill out the PR template
- Link related issues

### PR Requirements

Before submitting a PR, ensure:
- ✅ All tests pass
- ✅ Code follows style guidelines
- ✅ Documentation is updated
- ✅ Commits are clear and atomic
- ✅ No merge conflicts
- ✅ PR description is complete

### PR Review Process

1. **Automated checks** - CI/CD runs tests and linting
2. **Code review** - Team member reviews your code
3. **Feedback** - Address any comments or suggestions
4. **Approval** - PR is approved by maintainer
5. **Merge** - PR is merged into main branch

## 📝 Coding Standards

### TypeScript/JavaScript

- Use TypeScript for all new code
- Follow ESLint and Prettier configurations
- Use meaningful variable and function names
- Write JSDoc comments for public APIs
- Prefer `const` over `let`, avoid `var`
- Use async/await over callbacks
- Handle errors properly with try-catch

**Example:**
```typescript
/**
 * Calculate trading fees for a deposit
 * @param amount - Deposit amount in USDC (6 decimals)
 * @param chainId - Target chain ID
 * @returns Fee breakdown with trading and relayer fees
 */
async calculateFees(
  amount: bigint,
  chainId: number
): Promise<FeeBreakdown> {
  try {
    // Implementation
  } catch (error) {
    logger.error('Failed to calculate fees', { error });
    throw error;
  }
}
```

### Solidity

- Follow Solidity style guide
- Use Foundry for testing
- Document functions with NatSpec
- Optimize gas usage
- Use events for important state changes
- Include security considerations

**Example:**
```solidity
/// @notice Reserves funds in escrow with fee cap
/// @param orderId Unique order identifier
/// @param amount Principal amount in USDC
/// @param feeCap Maximum fee to charge
/// @return success Whether reservation succeeded
function reserve(
    bytes32 orderId,
    uint256 amount,
    uint256 feeCap
) external returns (bool success) {
    // Implementation
}
```

### File Structure

```
backend/
├── src/
│   ├── api/          # API route handlers
│   ├── services/     # Business logic
│   ├── routes/       # Route definitions
│   ├── utils/        # Utility functions
│   ├── types/        # TypeScript types
│   ├── db/           # Database models
│   └── tests/        # Test files
├── scripts/          # Utility scripts
└── docs/             # Documentation

contracts/
├── src/              # Solidity contracts
├── test/             # Foundry tests
├── script/           # Deployment scripts
└── docs/             # Contract documentation
```

## 🧪 Testing Guidelines

### Unit Tests

- Test individual functions in isolation
- Mock external dependencies
- Use descriptive test names
- Cover edge cases and error conditions

```typescript
describe('FeeCalculator', () => {
  describe('calculateFees', () => {
    it('should calculate correct trading fee for $100 deposit', async () => {
      const amount = 100_000000n; // $100 USDC
      const fees = await feeCalculator.calculateFees(amount);
      
      expect(fees.tradingFee).toBe(100000n); // 0.1% = $0.10
    });
    
    it('should throw error for zero amount', async () => {
      await expect(
        feeCalculator.calculateFees(0n)
      ).rejects.toThrow('Amount must be positive');
    });
  });
});
```

### Integration Tests

- Test interaction between components
- Use test database/blockchain
- Clean up after each test

### E2E Tests

- Test complete user flows
- Use real-world scenarios
- Verify system behavior

### Test Coverage

Maintain at least 80% test coverage:
```bash
npm run test:coverage
```

## 📜 Commit Message Guidelines

We follow [Conventional Commits](https://www.conventionalcommits.org/):

### Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

### Types

- `feat` - New feature
- `fix` - Bug fix
- `docs` - Documentation changes
- `style` - Code style changes (formatting)
- `refactor` - Code refactoring
- `perf` - Performance improvements
- `test` - Adding or updating tests
- `chore` - Maintenance tasks
- `ci` - CI/CD changes

### Examples

```bash
# Feature
feat(deposit): add fee calculation service

# Bug fix
fix(redemption): correct USDC transfer to user EOA

# Documentation
docs(readme): update installation instructions

# Multiple changes
feat(api): add deposit and redemption endpoints

- Add /aggregator/quote endpoint
- Add /aggregator/deposit endpoint
- Add /predifi/redeem endpoint
- Update Swagger documentation

Closes #123
```

### Guidelines

- Use imperative mood ("add" not "added")
- Keep subject line under 72 characters
- Separate subject from body with blank line
- Explain *what* and *why* in body, not *how*
- Reference issues with "Closes #123"

## 🌟 Areas We Need Help

### High Priority

- [ ] Frontend development (React/Next.js)
- [ ] Mobile app (React Native)
- [ ] Additional venue integrations
- [ ] Performance optimization
- [ ] Documentation improvements

### Medium Priority

- [ ] API rate limiting enhancements
- [ ] WebSocket optimizations
- [ ] Analytics dashboard
- [ ] Internationalization (i18n)

### Good First Issues

Look for issues labeled `good first issue` - these are perfect for newcomers!

## 💬 Community

### Communication Channels

- **Discord** - [Join our server](https://discord.gg/predifi)
- **Twitter** - [@predifi_com](https://twitter.com/predifi_com)
- **GitHub Discussions** - Ask questions, share ideas
- **Email** - admin@predifi.com

### Getting Help

- Check existing issues and documentation first
- Ask in Discord for quick questions
- Create GitHub issue for bugs/features
- Email for private/security concerns

### Code Review

- Be respectful and constructive
- Focus on the code, not the person
- Explain the "why" behind suggestions
- Praise good solutions
- Learn from others

## 🎓 Learning Resources

### Prediction Markets
- [Polymarket Docs](https://docs.polymarket.com)
- [Limitless Docs](https://docs.limitless.exchange)

### Cross-Chain
- [Circle CCTP](https://developers.circle.com/stablecoins/docs/cctp-getting-started)
- [LayerZero Docs](https://layerzero.gitbook.io)

### Smart Contracts
- [Foundry Book](https://book.getfoundry.sh)
- [OpenZeppelin Contracts](https://docs.openzeppelin.com/contracts)

### TypeScript
- [TypeScript Handbook](https://www.typescriptlang.org/docs/handbook/intro.html)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices)

## 📄 License

By contributing to Predifi, you agree that your contributions will be licensed under the MIT License.

## 🙏 Thank You

Thank you for contributing to Predifi! Every contribution, no matter how small, helps make prediction markets more accessible and efficient.

---

**Questions?** Reach out on [Discord](https://discord.gg/predifi) or email us at admin@predifi.com

**Happy Contributing! 🚀**
