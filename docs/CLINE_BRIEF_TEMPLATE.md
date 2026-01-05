# CLINE_BRIEF.md Template

Use this template to create handoff documents from your Research and Solution Architect agents to Cline.

---

# Implementation Brief: [Project Name]

**Date**: [Date]  
**Version**: 1.0  
**Based on**: 
- Research document: [filename]
- Architecture document: [filename]

---

## 1. Project Overview

**Purpose**: [What this project does - 2-3 sentences]

**Target Users**: [Who will use this]

**Key Features**:
- [Feature 1]
- [Feature 2]
- [Feature 3]

**Success Criteria**:
- [ ] [Measurable outcome 1]
- [ ] [Measurable outcome 2]
- [ ] [Measurable outcome 3]

---

## 2. Technology Stack

**From Architecture Document - Use Exactly These**:

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| Frontend | [e.g., React] | [18.x] | [UI rendering] |
| Backend | [e.g., Node.js] | [20 LTS] | [API server] |
| Database | [e.g., PostgreSQL] | [15.x] | [Data storage] |
| Cache | [e.g., Redis] | [7.x] | [Performance] |
| Auth | [e.g., JWT] | - | [Authentication] |
| Testing | [e.g., Jest] | - | [Test framework] |
| Deployment | [e.g., Docker] | - | [Containerization] |

**Required NPM Packages**:
```bash
# Core dependencies
npm install [package1] [package2] [package3]

# Dev dependencies
npm install -D [dev-package1] [dev-package2]
```

---

## 3. Project Structure

**Implement This Exact Structure**:

```
[project-name]/
├── src/
│   ├── [folder1]/
│   │   ├── [file1.ts]
│   │   ├── [file2.ts]
│   │   └── [subfolder]/
│   ├── [folder2]/
│   ├── common/
│   ├── config/
│   └── main.ts
├── test/
├── docker/
├── .env.example
├── package.json
├── tsconfig.json
└── README.md
```

**Key Folders**:
- `src/[folder1]/`: [Purpose of this folder]
- `src/[folder2]/`: [Purpose of this folder]
- `common/`: [Shared utilities]
- `config/`: [Configuration files]

---

## 4. Database Schema

**Implement These Tables/Entities**:

### Table/Entity: [Name1]

**SQL Schema** (if applicable):
```sql
CREATE TABLE [table_name] (
    id UUID PRIMARY KEY DEFAULT gen_random_uuid(),
    [column1] VARCHAR(255) NOT NULL,
    [column2] TEXT,
    created_at TIMESTAMP DEFAULT NOW(),
    updated_at TIMESTAMP DEFAULT NOW()
);

CREATE INDEX idx_[table]_[column] ON [table]([column]);
```

**OR ORM Entity** (if using TypeORM/Prisma/etc):
```typescript
// Paste exact entity definition from architecture
```

**Relationships**:
- [Relationship description]

---

### Table/Entity: [Name2]
[Repeat structure above]

---

## 5. API Specifications

**Implement These Endpoints Exactly**:

### Endpoint Group: [e.g., Authentication]

#### POST /auth/register
**Purpose**: User registration

**Request Body**:
```json
{
  "email": "user@example.com",
  "password": "securePassword123",
  "firstName": "John",
  "lastName": "Doe"
}
```

**Response (201 Created)**:
```json
{
  "id": "uuid",
  "email": "user@example.com",
  "firstName": "John",
  "lastName": "Doe",
  "createdAt": "2025-01-05T12:00:00Z"
}
```

**Response (400 Bad Request)**:
```json
{
  "statusCode": 400,
  "message": "Validation failed",
  "errors": [
    "email must be a valid email",
    "password must be at least 8 characters"
  ]
}
```

**Validation Rules**:
- Email: Valid email format, unique
- Password: Minimum 8 characters, must contain uppercase, lowercase, number
- FirstName/LastName: Optional, max 100 characters

**Implementation Notes**:
- Hash password with bcrypt (12 rounds)
- Don't return password in response
- Validate email uniqueness before creating user

---

#### POST /auth/login
**Purpose**: User login

[Similar detailed structure]

---

### Endpoint Group: [e.g., Resources]
[Repeat structure for all endpoints]

---

## 6. Component/Module Specifications

### Component/Module: [Name]

**Location**: `src/[path]/[filename]`

**Purpose**: [What this component does]

**Dependencies**:
- [Dependency 1]
- [Dependency 2]

**Interface/Class Structure**:
```typescript
// Define exact interface from architecture
export class [ComponentName] {
  // Properties
  private [property]: [type];
  
  // Constructor
  constructor([dependencies]) {}
  
  // Methods to implement
  async [method1]([params]): Promise<[ReturnType]> {
    // Implementation notes
  }
  
  async [method2]([params]): Promise<[ReturnType]> {
    // Implementation notes
  }
}
```

**Implementation Requirements**:
- [Requirement 1]
- [Requirement 2]
- [Requirement 3]

**Error Handling**:
- Throw [ErrorType] when [condition]
- Return null when [condition]
- Log errors with [format]

---

## 7. Implementation Constraints

### Must Use
- [Pattern/library 1]: [Why]
- [Pattern/library 2]: [Why]
- [Pattern/library 3]: [Why]

### Must Not Use
- ❌ [Anti-pattern 1]: [Why]
- ❌ [Anti-pattern 2]: [Why]

### Code Style
- Use TypeScript strict mode
- Follow [style guide - e.g., Airbnb, Standard]
- Use async/await (no callbacks or .then())
- Prefer functional programming patterns
- Use dependency injection

### Security Requirements
- Never log sensitive data (passwords, tokens, API keys)
- Validate all user inputs
- Sanitize outputs to prevent XSS
- Use parameterized queries (prevent SQL injection)
- Store secrets in environment variables only

### Performance Requirements
- API responses: < [X]ms p95
- Database queries: Add indexes for all foreign keys
- Implement caching for [specify what to cache]
- Use connection pooling for database

### Testing Requirements
- Unit tests for all services (80%+ coverage)
- Integration tests for all API endpoints
- E2E tests for critical user flows
- Mock external dependencies
- Test error cases and edge cases

---

## 8. Implementation Phases

### Phase 1: Foundation (Days 1-[X])

**Goal**: Set up project infrastructure

**Tasks**:
- [ ] Initialize project ([framework] setup)
- [ ] Configure [database] with [ORM]
- [ ] Set up basic folder structure
- [ ] Install core dependencies
- [ ] Create [config files]
- [ ] Set up development environment

**Deliverables**:
- Project runs locally
- Database connection working
- Basic structure in place

**Validation**:
```bash
npm run dev  # Should start without errors
npm run test # Should run (even if no tests yet)
```

---

### Phase 2: [Module/Feature Name] (Days [X]-[Y])

**Goal**: [What this phase achieves]

**Tasks**:
- [ ] Create [component/module 1]
- [ ] Implement [feature 1]
- [ ] Write unit tests for [component 1]
- [ ] Create API endpoint [endpoint 1]
- [ ] Test integration with [dependency]

**Deliverables**:
- [Specific deliverable 1]
- [Specific deliverable 2]

**Validation**:
- [How to verify this phase is complete]

---

### Phase 3: [Next Module/Feature]
[Repeat structure]

---

## 9. Example Implementations

### Example 1: [Component Name]

**From Architecture Document**:

```typescript
// Paste exact example from architecture
// This shows the expected style and structure

import { Injectable } from '@nestjs/common';
import { [Dependencies] } from '[packages]';

@Injectable()
export class [ExampleService] {
  constructor(
    private readonly [dependency]: [Type],
  ) {}
  
  async [exampleMethod]([param]: [Type]): Promise<[ReturnType]> {
    // Detailed implementation example
    try {
      // Step 1: Validate input
      if (!param) {
        throw new BadRequestException('Param is required');
      }
      
      // Step 2: Business logic
      const result = await this.[dependency].[method](param);
      
      // Step 3: Transform and return
      return this.transformResult(result);
    } catch (error) {
      // Error handling
      this.logger.error(`Error in [method]: ${error.message}`);
      throw error;
    }
  }
}
```

**Implement all components following this pattern.**

---

### Example 2: [Another Component]
[Another detailed example]

---

## 10. Configuration Files

### .env.example

```bash
# Database
DATABASE_URL="postgresql://user:password@localhost:5432/dbname"

# Authentication
JWT_SECRET="your-jwt-secret-key"
JWT_EXPIRES_IN="15m"
REFRESH_TOKEN_SECRET="your-refresh-token-secret"
REFRESH_TOKEN_EXPIRES_IN="7d"

# Application
PORT=3000
NODE_ENV=development

# External Services
[SERVICE_API_KEY]="your-api-key"
```

---

### tsconfig.json (If TypeScript)

```json
{
  "compilerOptions": {
    "target": "ES2021",
    "module": "commonjs",
    "strict": true,
    "esModuleInterop": true,
    "skipLibCheck": true,
    "forceConsistentCasingInFileNames": true,
    "outDir": "./dist",
    "rootDir": "./src",
    "baseUrl": "./",
    "paths": {
      "@/*": ["src/*"]
    }
  },
  "include": ["src/**/*"],
  "exclude": ["node_modules", "dist"]
}
```

---

### Docker Configuration (If applicable)

**Dockerfile**:
```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
RUN npm run build
CMD ["npm", "run", "start:prod"]
```

**docker-compose.yml**:
```yaml
version: '3.8'
services:
  app:
    build: .
    ports:
      - "3000:3000"
    environment:
      - DATABASE_URL=${DATABASE_URL}
    depends_on:
      - db
  
  db:
    image: postgres:15
    environment:
      - POSTGRES_DB=mydb
      - POSTGRES_USER=user
      - POSTGRES_PASSWORD=password
    volumes:
      - postgres_data:/var/lib/postgresql/data

volumes:
  postgres_data:
```

---

## 11. Testing Strategy

### Unit Tests

**Location**: `[test_directory]/unit/`

**Coverage Requirements**: 80%+ for all services

**Pattern to Follow**:
```typescript
// Example: auth.service.spec.ts
describe('AuthService', () => {
  let service: AuthService;
  let mockUserRepository: jest.Mocked<UserRepository>;
  
  beforeEach(() => {
    mockUserRepository = createMock<UserRepository>();
    service = new AuthService(mockUserRepository);
  });
  
  describe('register', () => {
    it('should create a new user with hashed password', async () => {
      // Arrange
      const input = { email: 'test@example.com', password: 'password123' };
      
      // Act
      const result = await service.register(input);
      
      // Assert
      expect(result.email).toBe(input.email);
      expect(result.password).not.toBe(input.password); // Hashed
      expect(mockUserRepository.save).toHaveBeenCalled();
    });
    
    it('should throw error if email already exists', async () => {
      // Test error case
    });
  });
});
```

### Integration Tests

**Location**: `[test_directory]/integration/`

**Test API Endpoints**:
```typescript
describe('POST /auth/register', () => {
  it('should register new user successfully', async () => {
    const response = await request(app)
      .post('/auth/register')
      .send({
        email: 'test@example.com',
        password: 'password123'
      });
    
    expect(response.status).toBe(201);
    expect(response.body).toHaveProperty('id');
  });
});
```

---

## 12. Documentation Requirements

### README.md Structure

```markdown
# [Project Name]

[Brief description]

## Features
- [Feature 1]
- [Feature 2]

## Tech Stack
[List from section 2]

## Prerequisites
- Node.js 20+
- PostgreSQL 15+
- [Others]

## Installation

```bash
# Clone repository
git clone [repo]

# Install dependencies
npm install

# Configure environment
cp .env.example .env
# Edit .env with your values

# Run database migrations
npm run migrate

# Start development server
npm run dev
```

## API Documentation
API documentation available at: http://localhost:3000/api/docs

## Testing
```bash
npm run test           # Unit tests
npm run test:e2e       # E2E tests
npm run test:cov       # Coverage report
```

## Deployment
[Deployment instructions]
```

### API Documentation

Generate with Swagger/OpenAPI:
- Add swagger decorators to all controllers
- Generate at `/api/docs`
- Include request/response examples

---

## 13. Research Insights Integration

**Key Findings from Research Agent**:

### [Insight Category 1]
- **Finding**: [What research found]
- **Implementation**: [How to apply this]
- **Rationale**: [Why this matters]

### [Insight Category 2]
[Repeat]

---

## 14. Success Criteria & Validation

### Functional Completeness
- [ ] All API endpoints implemented and tested
- [ ] All database entities created and migrated
- [ ] All business logic implemented
- [ ] Authentication/authorization working
- [ ] Error handling comprehensive

### Quality Gates
- [ ] Unit test coverage > 80%
- [ ] All integration tests passing
- [ ] No TypeScript errors
- [ ] No ESLint errors
- [ ] API documentation generated

### Performance Validation
- [ ] API response times < [X]ms
- [ ] Database queries optimized (indexes added)
- [ ] Caching implemented where specified
- [ ] Load testing completed (if applicable)

### Security Validation
- [ ] All inputs validated
- [ ] SQL injection prevented (parameterized queries)
- [ ] XSS prevented (output sanitization)
- [ ] Secrets in environment variables only
- [ ] Authentication protecting sensitive endpoints

### Documentation Completeness
- [ ] README with setup instructions
- [ ] API documentation (Swagger/Postman)
- [ ] Code comments for complex logic
- [ ] Environment variables documented

---

## 15. Known Issues & Limitations

**From Architecture Document**:
- [Limitation 1 and workaround]
- [Limitation 2 and workaround]

**Trade-offs Made**:
- [Trade-off 1]: Chose [A] over [B] because [reason]
- [Trade-off 2]: [Description]

---

## 16. Next Steps After Implementation

**Phase 2 Features** (Post-MVP):
- [Feature to add later]
- [Feature to add later]

**Optimization Opportunities**:
- [Optimization 1]
- [Optimization 2]

**Scaling Considerations**:
- [When to consider X]
- [When to consider Y]

---

## 17. Appendix

### Useful Commands

```bash
# Development
npm run dev              # Start dev server
npm run build            # Build for production
npm run start:prod       # Start production server

# Database
npm run migrate          # Run migrations
npm run migrate:rollback # Rollback last migration
npm run seed             # Seed database

# Testing
npm run test             # Run tests
npm run test:watch       # Watch mode
npm run test:cov         # Coverage report

# Linting
npm run lint             # Check code style
npm run lint:fix         # Auto-fix issues
```

### Reference Links
- Architecture Document: [link]
- Research Document: [link]
- Technology Documentation: [links]

---

**Implementation Ready**: All specifications from research and architecture 
documents have been consolidated into this actionable implementation brief.

**For Cline**: Read this document thoroughly. Implement each phase sequentially. 
Ask for approval before moving to the next phase. Follow all constraints and 
patterns specified. Reference the example implementations for code style.
