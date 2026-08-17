# Custom Security Rules Guide

## Creating a Custom Rule
```javascript
module.exports = {
    id: 'custom-001',
    name: 'No hardcoded API keys',
    severity: 'critical',
    pattern: /(api[_-]?key|secret|token)s*[:=]s*['"][A-Za-z0-9]{20,}['"]/gi,
    message: 'Hardcoded API key detected. Use environment variables instead.',
    fix: 'Move to .env file and use process.env.API_KEY'
};
```

## Rule Severity Levels
| Level | Score Impact | Action |
|-------|-------------|--------|
| Critical | -20 | Fails scan immediately |
| High | -10 | Major warning |
| Medium | -5 | Warning |
| Low | -2 | Info/suggestion |

## Common Custom Rules
1. **No console.log in production** - Remove debug statements
2. **SQL injection check** - Detect string concatenation in queries
3. **CORS wildcard** - Flag `Access-Control-Allow-Origin: *`
4. **Dependency age** - Warn if packages are 2+ years old
5. **License check** - Flag GPL dependencies in commercial projects

## Ignoring Rules
```json
// .guardrailrc
{
    "ignore": ["rule-id-001"],
    "exclude": ["node_modules/", "dist/", "*.test.js"]
}
```
