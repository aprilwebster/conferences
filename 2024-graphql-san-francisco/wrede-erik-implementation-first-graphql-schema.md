
# Executive Summary

This document explores the concept of **Implementation-First GraphQL** as presented at GraphQL Conf 2024. The approach prioritizes deriving GraphQL schemas from implementation rather than starting with predefined schemas (Schema-First) or writing both code and schema simultaneously (Code-First). The presentation highlighted several key benefits and challenges of using Implementation-First for GraphQL schema design.

**Key Benefits:**
1. **Intuitive and fast**: Implementation-First leverages native language features, making it easier to work directly within the codebase and avoids the need for code generators.
2. **Consistency**: There is no duplication between resolvers and type definitions, ensuring a single source of truth.
3. **Type safety**: By using native types, the Implementation-First approach ensures that the generated schema is type-safe by design.
4. **Production-ready**: With proper tools and frameworks like Strawberry, HotChocolate, and Grats, Implementation-First GraphQL is viable for production environments.

**Challenges:**
1. **Learning Curve**: Developers unfamiliar with Implementation-First may initially find it harder to understand compared to Schema-First.
2. **Framework Support**: Implementation-First is supported by some, but not all, GraphQL frameworks, which might limit its use depending on the project needs.


# Notes

1. **Schema-First vs Code-First**: 
   - Schema-First involves writing the GraphQL schema manually, then implementing the resolvers separately. It may lead to duplication and inconsistencies between schema and resolver types.
   - Code-First generates GraphQL types from the code, but it can also introduce duplication and lacks the strong consistency guarantees between resolvers and schema.
   
2. **Implementation-First**: 
   - In this approach, the schema is derived from the implementation using annotations or reflections. It ensures that schema and resolvers are consistent by design.
   - Frameworks supporting this method, such as Strawberry, HotChocolate, and Grats, provide built-in type safety.

3. **Key Frameworks**:
   - **Strawberry** (Python) and **HotChocolate** (C#) are popular frameworks supporting Implementation-First with annotations and type safety.
   - **Grats** offers strong consistency between resolvers and schema definitions using annotations.

4. **Consistency Benefits**:
   - In Implementation-First, there’s no risk of mismatch between the resolver's return type and the schema's expected type since the schema is automatically generated based on the implementation.

5. **Use Cases**:
   - Ideal for projects that are rapidly evolving where the schema is likely to change frequently.
   - Helpful when working in environments with strong type safety requirements, as it ensures that the implementation and schema are always in sync.


# Recommendations

## When to Use Implementation-First Instead of Schema-First
1. **Projects with frequent schema changes**: Since the schema is derived directly from the implementation, it is well-suited for projects where the schema is expected to change often. This avoids the need to manually synchronize changes between the schema and code.
   
2. **Teams prioritizing type safety**: If type safety and consistency between resolvers and schema are a priority, Implementation-First provides strong guarantees that all fields and methods exposed are type-safe and consistent with the schema.
   
3. **Small to medium-sized projects**: For projects with more contained domain models, the Implementation-First approach simplifies development by reducing duplication and avoiding the need for separate schema maintenance.

4. **Framework ecosystem**: Consider using Implementation-First when using a supported framework like Strawberry, HotChocolate, or Grats, especially when the native language (e.g., Python, C#) plays a central role in development.
