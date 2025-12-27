# Prioritized Test Coverage Improvements

**Generated:** December 27, 2025  
**Based on:** JaCoCo Coverage Analysis

This document provides a prioritized list of test coverage improvements for subsequent phases of the test improvement initiative.

---

## Priority Legend

| Priority | Description | Timeline |
|----------|-------------|----------|
| **Critical** | Security/business-critical functionality with no coverage | Phase 2 (Immediate) |
| **High** | Core functionality with significant gaps | Phase 2-3 |
| **Medium** | Supporting functionality with partial coverage | Phase 3-4 |
| **Low** | Nice-to-have improvements | Phase 4+ |

---

## Phase 2: Critical Improvements (Immediate)

### 1. GraphQL Article Operations
**Priority:** Critical  
**Current Coverage:** 0%  
**Estimated Effort:** 2 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test getFeed() query | ArticleDatafetcher.java | 42-86 |
| Test userFeed() query | ArticleDatafetcher.java | 88-136 |
| Test userFavorites() query | ArticleDatafetcher.java | 138-190 |
| Test userArticles() query | ArticleDatafetcher.java | 192-243 |
| Test getArticles() query | ArticleDatafetcher.java | 245-298 |
| Test findArticleBySlug() query | ArticleDatafetcher.java | 342-357 |
| Test createArticle() mutation | ArticleMutation.java | 35-51 |
| Test updateArticle() mutation | ArticleMutation.java | 53-70 |
| Test favoriteArticle() mutation | ArticleMutation.java | 72-83 |
| Test unfavoriteArticle() mutation | ArticleMutation.java | 85-100 |
| Test deleteArticle() mutation | ArticleMutation.java | 102-114 |

### 2. GraphQL User Operations
**Priority:** Critical  
**Current Coverage:** 0%  
**Estimated Effort:** 1 day

| Task | File | Lines to Cover |
|------|------|----------------|
| Test createUser() mutation | UserMutation.java | 36-53 |
| Test login() mutation | UserMutation.java | 55-67 |
| Test updateUser() mutation | UserMutation.java | 69-92 |
| Test getCurrentUser() utility | SecurityUtil.java | 10-18 |

### 3. GraphQL Comment Operations
**Priority:** Critical  
**Current Coverage:** 0%  
**Estimated Effort:** 1 day

| Task | File | Lines to Cover |
|------|------|----------------|
| Test createComment() mutation | CommentMutation.java | 31-47 |
| Test removeComment() mutation | CommentMutation.java | 49-67 |
| Test comment queries | CommentDatafetcher.java | All methods |

### 4. GraphQL Profile & Relation Operations
**Priority:** Critical  
**Current Coverage:** 0%  
**Estimated Effort:** 0.5 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test profile queries | ProfileDatafetcher.java | All methods |
| Test follow/unfollow mutations | RelationMutation.java | All methods |
| Test me queries | MeDatafetcher.java | All methods |

### 5. GraphQL Exception Handling
**Priority:** Critical  
**Current Coverage:** 3%  
**Estimated Effort:** 0.5 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test onException() handler | GraphQLCustomizeExceptionHandler.java | 30-68 |
| Test getErrorsAsData() | GraphQLCustomizeExceptionHandler.java | 70-93 |
| Test getParam() utility | GraphQLCustomizeExceptionHandler.java | 95-102 |

---

## Phase 3: High Priority Improvements

### 6. ArticleCommandService Tests
**Priority:** High  
**Current Coverage:** 15%  
**Estimated Effort:** 0.5 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test createArticle() with valid params | ArticleCommandService.java | 18-28 |
| Test createArticle() with empty tag list | ArticleCommandService.java | 18-28 |
| Test updateArticle() with valid params | ArticleCommandService.java | 30-37 |
| Test validation error scenarios | ArticleCommandService.java | All |

### 7. UpdateUserValidator Edge Cases
**Priority:** High  
**Current Coverage:** 62.5% branch  
**Estimated Effort:** 0.5 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test duplicate email validation | UserService.java | 90-96 |
| Test duplicate username validation | UserService.java | 97-102 |
| Test combined duplicate scenario | UserService.java | 87-104 |

### 8. CursorPageParameter Boundary Tests
**Priority:** High  
**Current Coverage:** 13.3% branch  
**Estimated Effort:** 0.5 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test limit > MAX_LIMIT (1000) | CursorPageParameter.java | 34-35 |
| Test limit = 0 | CursorPageParameter.java | 36-38 |
| Test negative limit | CursorPageParameter.java | 33-39 |
| Test Direction.PREV pagination | CursorPageParameter.java | 21-23 |

### 9. CommentQueryService Improvements
**Priority:** High  
**Current Coverage:** 47%  
**Estimated Effort:** 0.5 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test findById() with non-existent comment | CommentQueryService.java | Edge cases |
| Test findByArticleId() pagination | CommentQueryService.java | Edge cases |

---

## Phase 4: Medium Priority Improvements

### 10. DateTimeHandler Edge Cases
**Priority:** Medium  
**Current Coverage:** 52.2%  
**Estimated Effort:** 0.25 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test getResult(ResultSet, int) | DateTimeHandler.java | 33-37 |
| Test getResult(CallableStatement, int) | DateTimeHandler.java | 39-43 |
| Test null timestamp handling | DateTimeHandler.java | All getResult methods |

### 11. InvalidRequestException Tests
**Priority:** Medium  
**Current Coverage:** 0%  
**Estimated Effort:** 0.25 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test constructor | InvalidRequestException.java | 9-12 |
| Test getErrors() | InvalidRequestException.java | 14-16 |

### 12. CustomizeExceptionHandler Edge Cases
**Priority:** Medium  
**Current Coverage:** 68.7%  
**Estimated Effort:** 0.25 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test handleInvalidRequest() | CustomizeExceptionHandler.java | 27-48 |
| Test getParam() with single segment | CustomizeExceptionHandler.java | 101-108 |

### 13. AuthorizationService Edge Cases
**Priority:** Medium  
**Current Coverage:** 75% branch  
**Estimated Effort:** 0.25 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test canWriteComment() - article owner deleting other's comment | AuthorizationService.java | 12-14 |

### 14. TagsApi Improvements
**Priority:** Medium  
**Current Coverage:** 50%  
**Estimated Effort:** 0.25 days

| Task | File | Lines to Cover |
|------|------|----------------|
| Test getTags() endpoint | TagsApi.java | All |

---

## Phase 5: Low Priority Improvements

### 15. Domain Entity Branch Coverage
**Priority:** Low  
**Estimated Effort:** 0.5 days

| Entity | Current Branch Coverage | Target |
|--------|------------------------|--------|
| Article | 41.2% | 80% |
| User | 47.8% | 80% |
| Comment | 35.7% | 80% |
| ArticleFavorite | 31.8% | 80% |
| FollowRelation | 31.8% | 80% |
| Tag | 42.9% | 80% |

### 16. JaCoCo Configuration Improvements
**Priority:** Low  
**Estimated Effort:** 0.25 days

| Task | Description |
|------|-------------|
| Exclude Lombok-generated code | Add exclusion rules for getters/setters/equals/hashCode |
| Exclude DGS-generated types | Add exclusion for io.spring.graphql.types package |
| Set coverage thresholds | Configure minimum coverage requirements |

---

## Effort Summary

| Phase | Priority | Estimated Days | Coverage Impact |
|-------|----------|----------------|-----------------|
| Phase 2 | Critical | 5 days | +25-30% overall |
| Phase 3 | High | 2 days | +5-10% overall |
| Phase 4 | Medium | 1 day | +3-5% overall |
| Phase 5 | Low | 0.75 days | +2-3% overall |
| **Total** | | **8.75 days** | **+35-48% overall** |

---

## Expected Coverage After All Phases

| Metric | Current | After Phase 2 | After All Phases |
|--------|---------|---------------|------------------|
| Instructions | 33.25% | ~60% | ~75% |
| Branches | 16.40% | ~40% | ~60% |
| Lines | 34.15% | ~65% | ~80% |

---

## Test Infrastructure Requirements

### For GraphQL Testing (Phase 2)

1. **DGS Test Framework Setup**
   ```groovy
   testImplementation 'com.netflix.graphql.dgs:graphql-dgs-spring-boot-starter-test:4.9.21'
   ```

2. **Base Test Class for GraphQL**
   - Similar to `TestWithCurrentUser` for REST tests
   - Mock authentication context
   - Provide test data fixtures

3. **Test Data Fixtures**
   - Extend `TestHelper` for GraphQL-specific data
   - Create reusable article/user/comment fixtures

### For Service Layer Testing (Phase 3)

1. **Extend DbTestBase**
   - Add validation testing utilities
   - Add boundary testing helpers

2. **Mock Configuration**
   - Configure validation mocks
   - Set up repository mocks for edge cases

---

## Success Criteria

Phase 2 is considered complete when:
- All GraphQL mutations have at least one happy path test
- All GraphQL queries have at least one happy path test
- GraphQL authentication scenarios are tested
- Overall instruction coverage reaches 55%+

Phase 3 is considered complete when:
- ArticleCommandService has 80%+ coverage
- UpdateUserValidator has 90%+ branch coverage
- CursorPageParameter has 80%+ branch coverage
- Overall instruction coverage reaches 65%+

Phase 4 is considered complete when:
- All exception handlers have 80%+ coverage
- DateTimeHandler has 80%+ coverage
- Overall instruction coverage reaches 70%+

Phase 5 is considered complete when:
- Domain entities have 80%+ branch coverage
- JaCoCo exclusions are properly configured
- Overall instruction coverage reaches 75%+
