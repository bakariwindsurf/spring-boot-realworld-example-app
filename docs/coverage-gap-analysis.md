# Test Coverage Gap Analysis Report

**Generated:** December 27, 2025  
**Tool:** JaCoCo 0.8.8  
**Repository:** spring-boot-realworld-example-app

---

## Executive Summary

This report provides a comprehensive analysis of the current test coverage for the Spring Boot RealWorld application. The analysis identifies coverage gaps across all architectural layers and provides prioritized recommendations for improvement.

### Overall Coverage Metrics

| Metric | Covered | Total | Percentage |
|--------|---------|-------|------------|
| Instructions | 3,477 | 10,456 | **33.25%** |
| Branches | 146 | 890 | **16.40%** |
| Lines | 742 | 2,173 | **34.15%** |

---

## Coverage by Architectural Layer

### 1. API Layer (REST Controllers)

| Package | Instruction Coverage | Branch Coverage | Line Coverage |
|---------|---------------------|-----------------|---------------|
| io.spring.api | 97.0% | 83.3% | 96.6% |
| io.spring.api.security | 99.2% | 66.7% | 98.4% |
| io.spring.api.exception | 78.4% | 80.0% | 72.6% |

**Assessment:** The REST API layer has excellent coverage. The existing `@WebMvcTest` tests with RestAssured provide comprehensive testing of controller endpoints.

### 2. Application/Service Layer

| Package | Instruction Coverage | Branch Coverage | Line Coverage |
|---------|---------------------|-----------------|---------------|
| io.spring.application | 64.4% | 37.7% | 76.4% |
| io.spring.application.article | 20.5% | 100.0% | 26.7% |
| io.spring.application.user | 52.2% | 46.7% | 75.8% |
| io.spring.application.data | 25.7% | 0.0% | 98.4% |

**Assessment:** The service layer has moderate coverage with significant gaps in branch coverage. The `ArticleCommandService` and data classes have low instruction coverage.

### 3. Repository/Infrastructure Layer

| Package | Instruction Coverage | Branch Coverage | Line Coverage |
|---------|---------------------|-----------------|---------------|
| io.spring.infrastructure.repository | 94.0% | 80.0% | 94.4% |
| io.spring.infrastructure.service | 100.0% | N/A | 100.0% |
| io.spring.infrastructure.mybatis | 52.2% | 25.0% | 63.6% |

**Assessment:** Repository implementations have good coverage. The MyBatis type handler has gaps in edge case handling.

### 4. Core Domain Layer

| Package | Instruction Coverage | Branch Coverage | Line Coverage |
|---------|---------------------|-----------------|---------------|
| io.spring.core.article | 70.8% | 41.2% | 91.1% |
| io.spring.core.user | 71.8% | 47.8% | 94.3% |
| io.spring.core.comment | 69.0% | 35.7% | 100.0% |
| io.spring.core.favorite | 54.5% | 31.8% | 100.0% |
| io.spring.core.service | 88.0% | 75.0% | 66.7% |

**Assessment:** Domain entities have good line coverage but low branch coverage, indicating missing edge case tests.

### 5. GraphQL Layer

| Package | Instruction Coverage | Branch Coverage | Line Coverage |
|---------|---------------------|-----------------|---------------|
| io.spring.graphql | 4.7% | 0.0% | 1.9% |
| io.spring.graphql.exception | 3.0% | 0.0% | 3.2% |
| io.spring.graphql.types | 0.0% | 0.0% | 0.0% |

**Assessment:** **CRITICAL GAP** - The GraphQL layer has virtually no test coverage. This is the largest gap in the codebase.

---

## Detailed Gap Analysis

### Critical Priority Gaps

#### 1. GraphQL Layer - No Test Coverage
**Severity:** Critical  
**Estimated Effort:** High (3-5 days)

The entire GraphQL layer lacks test coverage:

| File | Lines Missed | Description |
|------|-------------|-------------|
| `ArticleDatafetcher.java` | 192/193 | All query resolvers untested |
| `ArticleMutation.java` | 52/53 | All mutations untested |
| `UserMutation.java` | 36/37 | User mutations untested |
| `CommentMutation.java` | 23/24 | Comment mutations untested |
| `CommentDatafetcher.java` | 53/54 | Comment queries untested |
| `ProfileDatafetcher.java` | 21/22 | Profile queries untested |
| `MeDatafetcher.java` | 21/22 | Me queries untested |
| `RelationMutation.java` | 26/27 | Relation mutations untested |
| `SecurityUtil.java` | 7/7 | Security utility untested |
| `GraphQLCustomizeExceptionHandler.java` | 59/61 | Exception handling untested |

**Specific Uncovered Code Sections:**
- `ArticleDatafetcher.java:42-86` - getFeed() method
- `ArticleDatafetcher.java:88-136` - userFeed() method
- `ArticleDatafetcher.java:138-190` - userFavorites() method
- `ArticleDatafetcher.java:192-243` - userArticles() method
- `ArticleDatafetcher.java:245-298` - getArticles() method
- `ArticleMutation.java:35-51` - createArticle() method
- `ArticleMutation.java:53-70` - updateArticle() method
- `ArticleMutation.java:72-83` - favoriteArticle() method
- `ArticleMutation.java:85-100` - unfavoriteArticle() method
- `ArticleMutation.java:102-114` - deleteArticle() method
- `UserMutation.java:36-53` - createUser() method
- `UserMutation.java:55-67` - login() method
- `UserMutation.java:69-92` - updateUser() method
- `SecurityUtil.java:10-18` - getCurrentUser() method

**Recommendation:** Create a new test class `GraphQLApiTest.java` using DGS testing framework to test all GraphQL operations.

---

### High Priority Gaps

#### 2. ArticleCommandService - Low Coverage
**Severity:** High  
**Estimated Effort:** Medium (1 day)  
**File:** `src/main/java/io/spring/application/article/ArticleCommandService.java`

| Metric | Missed | Covered | Coverage |
|--------|--------|---------|----------|
| Instructions | 34 | 6 | 15.0% |
| Lines | 14 | 1 | 6.7% |

**Uncovered Code Sections:**
- `ArticleCommandService.java:18-28` - createArticle() method
- `ArticleCommandService.java:30-37` - updateArticle() method

**Missing Test Scenarios:**
- Article creation with validation
- Article update with validation
- Edge cases for null/empty tag lists

---

#### 3. UpdateUserValidator - Partial Coverage
**Severity:** High  
**Estimated Effort:** Medium (0.5 days)  
**File:** `src/main/java/io/spring/application/user/UserService.java`

| Metric | Missed | Covered | Coverage |
|--------|--------|---------|----------|
| Instructions | 12 | 66 | 84.6% |
| Branches | 3 | 5 | 62.5% |

**Uncovered Code Sections:**
- `UserService.java:90-96` - Email validation error path
- `UserService.java:97-102` - Username validation error path

**Missing Test Scenarios:**
- Update user with duplicate email (should fail)
- Update user with duplicate username (should fail)
- Combined duplicate email and username scenario

---

#### 4. CursorPageParameter - Low Branch Coverage
**Severity:** High  
**Estimated Effort:** Low (0.5 days)  
**File:** `src/main/java/io/spring/application/CursorPageParameter.java`

| Metric | Missed | Covered | Coverage |
|--------|--------|---------|----------|
| Instructions | 124 | 54 | 30.3% |
| Branches | 26 | 4 | 13.3% |

**Uncovered Code Sections:**
- `CursorPageParameter.java:33-39` - setLimit() edge cases

**Missing Test Scenarios:**
- Limit exceeding MAX_LIMIT (1000)
- Limit of 0 or negative values
- Direction.PREV pagination

---

### Medium Priority Gaps

#### 5. DateTimeHandler - Partial Coverage
**Severity:** Medium  
**Estimated Effort:** Low (0.5 days)  
**File:** `src/main/java/io/spring/infrastructure/mybatis/DateTimeHandler.java`

| Metric | Missed | Covered | Coverage |
|--------|--------|---------|----------|
| Instructions | 32 | 35 | 52.2% |
| Branches | 6 | 2 | 25.0% |

**Uncovered Code Sections:**
- `DateTimeHandler.java:33-37` - getResult(ResultSet, int) method
- `DateTimeHandler.java:39-43` - getResult(CallableStatement, int) method

**Missing Test Scenarios:**
- Null timestamp handling in all getResult methods
- Column index-based result retrieval

---

#### 6. InvalidRequestException - No Coverage
**Severity:** Medium  
**Estimated Effort:** Low (0.25 days)  
**File:** `src/main/java/io/spring/api/exception/InvalidRequestException.java`

| Metric | Missed | Covered | Coverage |
|--------|--------|---------|----------|
| Instructions | 10 | 0 | 0.0% |
| Lines | 4 | 0 | 0.0% |

**Uncovered Code Sections:**
- `InvalidRequestException.java:9-12` - Constructor
- `InvalidRequestException.java:14-16` - getErrors() method

**Missing Test Scenarios:**
- Exception creation with validation errors
- Error retrieval

---

#### 7. CustomizeExceptionHandler - Partial Coverage
**Severity:** Medium  
**Estimated Effort:** Medium (0.5 days)  
**File:** `src/main/java/io/spring/api/exception/CustomizeExceptionHandler.java`

| Metric | Missed | Covered | Coverage |
|--------|--------|---------|----------|
| Instructions | 47 | 103 | 68.7% |
| Lines | 15 | 26 | 63.4% |

**Uncovered Code Sections:**
- `CustomizeExceptionHandler.java:27-48` - handleInvalidRequest() method (partial)
- `CustomizeExceptionHandler.java:101-108` - getParam() edge cases

**Missing Test Scenarios:**
- InvalidRequestException handling
- Property path parsing with single segment

---

#### 8. AuthorizationService - Partial Branch Coverage
**Severity:** Medium  
**Estimated Effort:** Low (0.25 days)  
**File:** `src/main/java/io/spring/core/service/AuthorizationService.java`

| Metric | Missed | Covered | Coverage |
|--------|--------|---------|----------|
| Instructions | 3 | 22 | 88.0% |
| Branches | 1 | 3 | 75.0% |

**Uncovered Code Sections:**
- `AuthorizationService.java:12-14` - canWriteComment() when user is article owner but not comment owner

**Missing Test Scenarios:**
- Article owner deleting another user's comment
- Non-owner attempting to delete comment

---

### Low Priority Gaps

#### 9. Data Classes - Lombok Generated Code
**Severity:** Low  
**Estimated Effort:** Low (optional)

The following data classes have low instruction coverage due to Lombok-generated methods (getters, setters, equals, hashCode, toString):

| Class | Instruction Coverage |
|-------|---------------------|
| ArticleData | 25.0% |
| ProfileData | 23.3% |
| CommentData | 22.8% |
| UserData | 22.1% |
| ArticleFavoriteCount | 14.4% |

**Recommendation:** Consider excluding Lombok-generated code from coverage reports or adding tests for equals/hashCode if business logic depends on them.

---

#### 10. Builder Classes - No Coverage
**Severity:** Low  
**Estimated Effort:** Low (optional)

Builder classes generated by Lombok have 0% coverage:
- `NewArticleParam.NewArticleParamBuilder`
- `UpdateUserParam.UpdateUserParamBuilder`

**Recommendation:** These are typically tested indirectly through service tests. Consider excluding from coverage metrics.

---

#### 11. GraphQL Types - Generated Code
**Severity:** Low  
**Estimated Effort:** N/A

The `io.spring.graphql.types` package contains DGS-generated types with 0% coverage. These are data transfer objects and don't require direct testing.

**Recommendation:** Exclude from coverage metrics using JaCoCo exclusion rules.

---

## Coverage Gaps by Component

### Article Management

| Area | Coverage Status | Priority |
|------|-----------------|----------|
| ArticleApi (REST) | Excellent (97%+) | N/A |
| ArticleCommandService | Poor (15%) | High |
| ArticleQueryService | Good (77%) | Medium |
| ArticleDatafetcher (GraphQL) | None (0%) | Critical |
| ArticleMutation (GraphQL) | None (0%) | Critical |
| Article entity | Good (75%) | Low |

### User Management

| Area | Coverage Status | Priority |
|------|-----------------|----------|
| UsersApi (REST) | Excellent (100%) | N/A |
| UserService | Moderate (61%) | High |
| UserMutation (GraphQL) | None (0%) | Critical |
| User entity | Good (87%) | Low |

### Comment System

| Area | Coverage Status | Priority |
|------|-----------------|----------|
| CommentsApi (REST) | Excellent (100%) | N/A |
| CommentQueryService | Moderate (47%) | Medium |
| CommentMutation (GraphQL) | None (0%) | Critical |
| CommentDatafetcher (GraphQL) | None (0%) | Critical |

### Profile Management

| Area | Coverage Status | Priority |
|------|-----------------|----------|
| ProfileApi (REST) | Excellent (96%) | N/A |
| ProfileQueryService | Good (91%) | Low |
| ProfileDatafetcher (GraphQL) | None (0%) | Critical |

### Tag Management

| Area | Coverage Status | Priority |
|------|-----------------|----------|
| TagsApi (REST) | Moderate (50%) | Medium |
| TagsQueryService | Excellent (100%) | N/A |
| TagDatafetcher (GraphQL) | Moderate (60%) | Medium |

---

## Authorization Testing Gaps

### Current Authorization Tests
The REST API tests cover basic authorization scenarios through `TestWithCurrentUser` base class.

### Missing Authorization Scenarios

1. **Article Authorization**
   - Non-owner attempting to update article (partially tested)
   - Non-owner attempting to delete article (partially tested)
   - GraphQL mutations with unauthorized users (not tested)

2. **Comment Authorization**
   - Article owner deleting other's comments (not tested)
   - Non-owner/non-author attempting to delete comment (partially tested)
   - GraphQL mutations with unauthorized users (not tested)

3. **Profile Authorization**
   - Following/unfollowing without authentication (partially tested)
   - GraphQL mutations without authentication (not tested)

---

## Recommendations

### Immediate Actions (Phase 2)

1. **Create GraphQL Test Infrastructure**
   - Set up DGS test framework
   - Create base test class similar to `TestWithCurrentUser`
   - Implement authentication mocking for GraphQL

2. **Add GraphQL Mutation Tests**
   - ArticleMutation tests (create, update, delete, favorite)
   - UserMutation tests (create, login, update)
   - CommentMutation tests (add, delete)
   - RelationMutation tests (follow, unfollow)

3. **Add GraphQL Query Tests**
   - ArticleDatafetcher tests (feed, articles, article by slug)
   - CommentDatafetcher tests
   - ProfileDatafetcher tests
   - MeDatafetcher tests

### Short-term Actions (Phase 3)

4. **Improve Service Layer Coverage**
   - ArticleCommandService validation tests
   - UpdateUserValidator edge case tests
   - CursorPageParameter boundary tests

5. **Add Error Handling Tests**
   - InvalidRequestException scenarios
   - GraphQLCustomizeExceptionHandler scenarios
   - CustomizeExceptionHandler edge cases

### Long-term Actions (Phase 4)

6. **Improve Branch Coverage**
   - Add edge case tests for domain entities
   - Test null handling in DateTimeHandler
   - Test pagination edge cases

7. **Configure Coverage Exclusions**
   - Exclude Lombok-generated code
   - Exclude DGS-generated types
   - Set coverage thresholds

---

## Appendix: JaCoCo Configuration

The following JaCoCo configuration was added to `build.gradle`:

```groovy
plugins {
    id 'jacoco'
}

jacoco {
    toolVersion = "0.8.8"
}

tasks.named('test') {
    useJUnitPlatform()
    finalizedBy jacocoTestReport
}

jacocoTestReport {
    dependsOn test
    reports {
        xml.required = true
        csv.required = true
        html.required = true
        html.outputLocation = layout.buildDirectory.dir('reports/jacoco/html')
    }
}
```

### Report Locations
- HTML Report: `build/reports/jacoco/html/index.html`
- XML Report: `build/reports/jacoco/test/jacocoTestReport.xml`
- CSV Report: `build/reports/jacoco/test/jacocoTestReport.csv`

---

## Summary

The Spring Boot RealWorld application has a solid testing foundation for the REST API layer but significant gaps in the GraphQL layer and some service components. The most critical finding is the complete lack of test coverage for GraphQL operations, which represents a significant portion of the application's functionality.

**Priority Order for Test Improvements:**
1. GraphQL layer tests (Critical - 0% coverage)
2. ArticleCommandService tests (High - 15% coverage)
3. UpdateUserValidator edge cases (High - 62.5% branch coverage)
4. CursorPageParameter boundary tests (High - 13.3% branch coverage)
5. Error handling tests (Medium)
6. Authorization edge cases (Medium)
7. Data class and utility coverage (Low)
