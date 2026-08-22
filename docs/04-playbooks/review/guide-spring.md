# Review Guide – Spring

> **Purpose:** technology-specific extension to the generic Code Review Book for Spring / Spring Boot implementation.

## Dependency Injection & Bean Design

* Are dependencies explicit and constructor-injected where practical?
* Are bean scopes appropriate?
* Is mutable state stored in singleton beans accidentally?
* Are lifecycle assumptions (`@PostConstruct`, shutdown hooks, lazy initialization) valid?
* Are circular dependencies being introduced or hidden?
* Are configuration values strongly typed and validated where material?

## Transaction Boundaries

* Is `@Transactional` placed at the correct application/service boundary?
* Are self-invocation/proxy limitations relevant?
* Is transaction propagation intentional?
* Are checked-exception rollback assumptions correct?
* Are remote calls or long-running work performed inside transactions unnecessarily?
* Could retries repeat partially committed side effects?

## REST / API Layer

* Are HTTP methods and status codes semantically correct?
* Are POST/PUT/PATCH semantics and idempotency intentional?
* Are request DTOs validated at the boundary?
* Are domain entities leaking directly through API contracts?
* Is error mapping consistent and safe?
* Are pagination/filter/sort inputs bounded?
* Are backward compatibility and API-version implications considered?

## Spring Security

* Is authorization enforced server-side and at the correct boundary?
* Are method-level and endpoint-level rules consistent?
* Could a new endpoint bypass existing security configuration?
* Are JWT/claims/roles interpreted correctly?
* Is tenant/user context trusted only from validated sources?
* Are CORS/CSRF assumptions appropriate to the application type?

## Persistence / JPA Integration

* Are lazy-loading assumptions safe outside transactions?
* Could Open Session / Open EntityManager in View hide N+1 or boundary problems?
* Are entity graphs/fetch joins used intentionally?
* Are cascades and orphan removal appropriate?
* Are entity lifecycle callbacks introducing hidden side effects?
* Are bulk updates bypassing persistence-context assumptions?

## Configuration & Environments

* Are defaults safe?
* Could profile-specific configuration create behavior differences not covered by tests?
* Are secrets referenced rather than embedded?
* Are feature flags/configuration changes backward compatible?
* Are startup failures preferable to silently invalid configuration where material?

## Resilience / Integrations

* Are timeouts defined for outbound calls?
* Are retries bounded, idempotent and applied to the right failures?
* Are circuit-breaker/fallback behaviors intentional?
* Are thread pools/executors bounded and observable?
* Are blocking calls introduced into reactive code paths?

## Testing Signals

* Are tests using the lightest useful Spring context?
* Is `@SpringBootTest` overused where slice/unit tests would be clearer and faster?
* Are security rules tested, not only controller happy paths?
* Are transaction semantics tested where they matter?
* Are mocks hiding important framework/integration behavior?

## AI-Specific Red Flags

Pay extra attention to AI-generated Spring code for:

* unnecessary annotations,
* broad `@Transactional` usage,
* magic configuration properties,
* controller/service/repository layer duplication,
* security rules assumed rather than verified,
* generated exception handlers that leak internal details,
* overuse of full-context tests.

> **Review principle:** Spring convenience must not hide transaction, security or lifecycle behavior from the reviewer.
