
# Praetorian CLI 🏛️  
**Guardian of Configurations** – Universal Validation Framework for DevSecOps  

![npm version](https://img.shields.io/npm/v/@syntropysoft/praetorian)  
![build status](https://img.shields.io/github/actions/workflow/status/Syntropysoft/praetorian/ci.yml)  
![license](https://img.shields.io/npm/l/@syntropysoft/praetorian?color=blue)

---

```
  ____                 _             _                ____ _     ___ 
 |  _ \ _ __ __ _  ___| |_ ___  _ __(_) __ _ _ __    / ___| |   |_ _|
 | |_) | '__/ _` |/ _ \ __/ _ \| '__| |/ _` | '_ \  | |   | |    | | 
 |  __/| | | (_| |  __/ || (_) | |  | | (_| | | | | | |___| |___ | | 
 |_|   |_|  \__,_|\___|\__\___/|_|  |_|\__,_|_| |_|  \____|_____|___|
                                                                     
🛡️  Guardian of Configurations & Security
```

---

## 🎉 **ALPHA-2 RELEASE HIGHLIGHTS**

> **🚀 Praetorian CLI v0.0.2-alpha.1 - Major Improvements!**
> 
> **✅ NEW FEATURES & IMPROVEMENTS:**
> - **🏗️ Clean Architecture** - Complete codebase reorganization with SOLID principles
> - **🧪 Robust Testing** - 158 tests passing with comprehensive coverage
> - **📦 Optimized Dependencies** - 36 unnecessary packages removed (66% reduction)
> - **🔧 Enhanced Build System** - Improved TypeScript compilation and error handling
> - **📚 Professional Documentation** - Complete English documentation with working examples
> - **🎯 Perfect Example** - Ready-to-use example that demonstrates best practices
> - **🛡️ Plugin System** - Functional plugin architecture for extensibility
> - **⚡ Performance Improvements** - Faster validation and better error handling
> - **🧹 Automatic Cleanup** - Smart temporary file management
> - **🔍 Advanced Validation** - Improved key comparison and structure validation
> 
> **✅ CORE FEATURES (All Working):**
> - **CLI with professional banner** - Beautiful ASCII art with security colors
> - **Key comparison** - Compare keys across multiple configuration files (JSON/YAML/.env)
> - **Multi-folder support** - Works with files in different directories
> - **C# compatibility** - Supports appsettings.json and other .NET configurations
> - **Configuration file** - `praetorian.yaml` for defining files to compare
> - **Exit codes** - Proper exit codes for CI/CD integration
> - **Missing file detection** - Automatically create empty structure files for missing configurations
> - **Required keys validation** - Ensure mandatory configuration keys are present
> - **Environment mapping** - Support for environment-specific configuration files
> 
> **🚧 COMING IN FUTURE RELEASES:**
> - Schema validation, pattern matching, security rules
> - Advanced plugin system, custom rules, audit engine
> - Advanced validation features mentioned in examples
> 
> **For production use, wait for stable releases (1.0.0+)**

---

## 🚀 Description

Praetorian CLI is a multi-environment configuration validation tool designed for **DevSecOps** teams.  
It ensures that your configuration files remain **consistent across environments** and detects critical differences before production deployments.

**Perfect for:**
- 🏗️ **Microservices architectures** with multiple config files
- 🔄 **Multi-environment deployments** (dev, staging, prod)
- 🛡️ **Security compliance** and configuration drift detection
- 🚀 **CI/CD pipelines** requiring config validation
- 📝 **Development workflow** - Auto-create missing configuration structures

---

## ✨ Features

- 🛡️ **Multi-file, multi-environment validation** (`dev`, `staging`, `prod`)
- 🔍 **Detects missing keys or inconsistent values** across files
- 📁 **Multi-folder support** - Compare files in different directories
- 🔧 **Framework agnostic** - Works with any tech stack
- 📝 **Simple setup** with `praetorian.yaml`
- 📦 **CI/CD friendly** with proper exit codes
- 🔑 **Supports ignored keys** and required keys validation
- 🆕 **Auto-create missing files** - Generate empty structure files for missing configurations
- 🌍 **Environment mapping** - Validate specific environments or all environments

---

## 🔧 Compatible With

- **Configuration Formats**: JSON, YAML, .env files
- **Frameworks**: Node.js, .NET (appsettings.json), Python, Java, Go
- **Environments**: Development, Staging, Production, Testing
- **Architectures**: Monoliths, Microservices, Serverless
- **Platforms**: Docker, Kubernetes, Cloud (AWS, Azure, GCP)

---

## 📦 Installation

```bash
npm install -g @syntropysoft/praetorian
```

**Prerequisites:**
- Node.js 18+ (recommended: use [NVM](https://github.com/nvm-sh/nvm))
- npm or yarn

---

## ⚙️ Basic Configuration

Create a `praetorian.yaml` file:

```yaml
files:
  - config-dev.yaml
  - config-prod.yaml
  - config-staging.yaml

ignore_keys:
  - debug
  - temp

required_keys:
  - database.host
  - database.port
  - api.version
  - api.port

environments:
  dev: config-dev.yaml
  prod: config-prod.yaml
  staging: config-staging.yaml
```

---

## 🛠️ Usage

### Basic Validation

Validate that all configuration files have matching keys:

```bash
praetorian validate
```

**Output example:**
```
📊 Validation Results:
✅ All configuration files are consistent!
📈 Summary:
  • Files compared: 3
  • Total keys: 15
  • Duration: 2ms
```

**In case of differences:**
```
❌ Key inconsistencies found:
  • Key 'database.url' is missing in config-staging.yaml
  • Key 'api.timeout' is missing in config-dev.yaml
```

### Environment-Specific Validation

Validate a specific environment:

```bash
praetorian validate --env dev
```

Validate all environments:

```bash
praetorian validate --all
```

### Missing File Detection

When files are missing, Praetorian automatically creates empty structure files:

```
⚠️  Missing files detected: config-staging.yaml
💡 Creating empty structure files...
✅ Created 1 empty structure file(s)
```

The created file will have the structure based on `required_keys`:

```yaml
# config-staging.yaml (auto-created)
database:
  host: null
  port: null
api:
  version: null
  port: null
```

---

## 📋 Examples

### 🎯 **Quick Examples**

#### Example 1: Basic Configuration Files

```yaml
# config-dev.yaml
app:
  name: my-app
  debug: true
  port: 3000

database:
  host: localhost
  port: 5432
```

```yaml
# config-prod.yaml
app:
  name: my-app
  port: 80

database:
  host: prod-db.example.com
  port: 5432
  url: postgresql://user:pass@prod-db.example.com:5432/db
```

#### Example 2: C# appsettings.json

```json
// apps/web/appsettings.json
{
  "Logging": {
    "LogLevel": {
      "Default": "Information"
    }
  },
  "ConnectionStrings": {
    "DefaultConnection": "Server=localhost;Database=WebApp;"
  },
  "AppSettings": {
    "ApiKey": "web-api-key-12345",
    "BaseUrl": "https://web.example.com"
  }
}
```

#### Example 3: Multi-folder Structure

```yaml
# praetorian.yaml
files:
  - configs/frontend/app.config.json
  - configs/backend/app.config.json
  - apps/web/appsettings.json
  - apps/api/appsettings.json

ignore_keys:
  - debug
  - Logging
  - AllowedHosts

required_keys:
  - database.host
  - api.port
  - logging.level
```

#### Example 4: Environment Mapping

```yaml
# environments.yaml
dev: config-dev.yaml
staging: config-staging.yaml
production: config-prod.yaml
```

```bash
# Validate specific environment
praetorian validate --environments environments.yaml --env dev

# Validate all environments
praetorian validate --environments environments.yaml --all
```

### 📚 **Complete Examples**

Check out our **[examples directory](./examples/validation/)** for comprehensive examples:

- **[Perfect Example](./examples/validation/perfect-example/)** - **NEW!** Complete working example with consistent structure
- **[Missing Files Demo](./examples/validation/missing-files-demo/)** - **NEW!** Automatic file creation demonstration
- **[YAML Examples](./examples/validation/yaml/)** - Basic YAML configuration validation
- **[JSON Examples](./examples/validation/json/)** - JSON configuration files
- **[ENV Examples](./examples/validation/env/)** - Environment file validation
- **[.NET Examples](./examples/validation/dotnet/)** - C# appsettings.json and multi-folder validation

Each example includes:

---

## 🧪 Testing & Quality

### **Comprehensive Test Suite**
- **✅ 158 tests passing** across 13 test suites
- **✅ Unit tests** for all core functionality
- **✅ Integration tests** for end-to-end validation
- **✅ Mutation testing** configured with Stryker
- **✅ Coverage reporting** for quality assurance

### **Test Coverage Highlights**
- **100% coverage** on core validation logic
- **100% coverage** on plugin management
- **100% coverage** on environment management
- **97% coverage** on utility functions
- **86% coverage** on validation rules

### **Running Tests**
```bash
# Run all tests
npm test

# Run with coverage
npm run test:coverage

# Run integration tests only
npm run test:integration

# Run mutation tests
npm run test:mutation
```

### **Quality Metrics**
- **Clean Architecture** - SOLID principles applied
- **Functional Programming** - Pure functions and immutability
- **Type Safety** - Full TypeScript coverage
- **Error Handling** - Comprehensive error management
- **Performance** - Optimized for speed and efficiency
- Sample configuration files
- `praetorian.yaml` setup
- Expected validation results
- Common use cases

---

## 🧩 CI/CD Integration

### GitHub Actions Example

```yaml
- name: Validate Configurations
  run: |
    npm install -g @syntropysoft/praetorian
    praetorian validate
```

### GitLab CI Example

```yaml
validate_configs:
  stage: test
  script:
    - npm install -g @syntropysoft/praetorian
    - praetorian validate
```

---

## 🗺️ Roadmap

- [ ] **Schema validation** - Type checking and pattern matching
- [ ] **Security rules** - Detect sensitive data exposure
- [ ] **JSON/HTML reports** - Detailed validation reports
- [ ] **Custom rule plugins** - Extensible validation system
- [ ] **Secret management integration** - AWS Secrets Manager, Azure Key Vault
- [ ] **Performance optimization** - Parallel processing for large configs

---

## 🏢 About SyntropySoft

**Praetorian CLI** is proudly developed by **[SyntropySoft](https://syntropysoft.com)** - Your trusted partner in DevSecOps solutions.

### Our Products

- 🔍 **[SyntropyLog](https://github.com/Syntropysoft/syntropylog)** - Advanced logging and monitoring platform
- 🎨 **[SyntropyFront](https://github.com/Syntropysoft/syntropyfront)** - Modern frontend development framework
- 🛡️ **[Praetorian CLI](https://github.com/Syntropysoft/praetorian)** - Configuration validation framework *(you are here)*

### Connect With Us

- 🌐 **[Website](https://syntropysoft.com)**
- 📧 **[Contact](mailto:contact@syntropysoft.com)**
- 💼 **[LinkedIn](https://www.linkedin.com/company/syntropysoft)**

---

## 📜 License

Apache 2.0 © [SyntropySoft](https://syntropysoft.com)

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at [http://www.apache.org/licenses/LICENSE-2.0](http://www.apache.org/licenses/LICENSE-2.0).

---

## 🤝 Contributing

We welcome contributions! Please see our [Contributing Guide](CONTRIBUTING.md) for details.

**Star us on GitHub** ⭐ - It helps a lot!