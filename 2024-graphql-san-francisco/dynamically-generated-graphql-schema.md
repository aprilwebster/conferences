
# Executive Summary

This document, presented by Emily Li at GraphQLConf 2024, discusses the implementation of a **Dynamically Generated GraphQL API** at Benchling. The API serves custom types and schemas tailored to each customer at runtime. This approach allows for **extensibility**, where types and relationships are modified dynamically, enabling a unique graph for every customer. 

Key challenges and solutions were presented, including strategies for managing **performance bottlenecks** and **scaling** a graph with over 40,000 enum members and 5,000 types. Benchling employs dynamic generation techniques using the **Strawberry** framework to define and resolve types on-the-fly. The focus is on leveraging **caching mechanisms** to enhance query performance.

**Key Benefits:**
1. **Custom Graphs**: Each customer's graph is unique, dynamically generated based on their custom types.
2. **Scalability**: The system handles over 40,000 enum members and 5,000 total types.
3. **Performance Optimization**: Techniques such as caching Strawberry SDL documents and using subgraph generation significantly improve performance.

**Challenges:**
1. **Introspection Speed**: Introspection originally took over 60 seconds due to the large graph size.
2. **Graph Mutability**: The mutable nature of the graph, where types can change at any time, adds complexity to the system.

Through a combination of **dynamic graph generation**, **forward references**, and **cache repair strategies**, Benchling successfully optimized their GraphQL API to serve unique, large-scale graphs to multiple customers with minimal latency.


# Notes

1. **Benchling's Use Case**: 
   - Benchling's platform, designed for scientific data, leverages a GraphQL API that dynamically generates types and graphs based on each customer’s custom data structures.
   - Each customer’s graph is unique due to custom types and highly connected relationships between these types.

2. **Dynamic Graph Generation**:
   - Custom types are combined with built-in types to form a unique schema for each customer.
   - Using the Strawberry framework, types are defined as Python dataclasses, and resolvers are dynamically generated for each type.
   
3. **Performance Challenges**:
   - **Introspection Performance**: Building the entire graph for introspection took more than 60 seconds.
   - **Graph Scale**: The graph contains 40,000+ enum members and 5,000+ types, significantly larger than typical GraphQL APIs.

4. **Mitigation Strategies**:
   - **Caching**: Type data and SDL documents are cached to reduce the introspection time to under 1 second.
   - **Subgraph Generation**: Only relevant parts of the graph are generated during a query, improving performance.
   
5. **Frameworks**:
   - Benchling uses the **Strawberry** framework to dynamically generate types and resolvers at runtime.


# Recommendations

## When and Why to Dynamically Generate an API with Custom Schemas

1. **Highly Customizable Use Cases**:
   - If your customers or users have unique data models and types, dynamically generating the schema allows each user to have a tailored API experience without extensive manual intervention.

2. **Mutable Data Models**:
   - For platforms where the types in the graph can change frequently or in real-time, dynamically generating the API avoids the need for redeployment whenever a type changes.

3. **Performance in Large-Scale Systems**:
   - When serving complex and highly connected graphs at scale (e.g., 40,000+ enum members), dynamically generating only relevant subgraphs and using caching strategies can significantly reduce query response time.

4. **Scientific or Data-Driven Applications**:
   - In environments like scientific research, where data models evolve, and each user might require different types, dynamic generation ensures flexibility and minimizes the need to manually adjust the schema for every new use case.

5. **When Flexibility and Extensibility are Key**:
   - Dynamic generation offers more flexibility compared to a static schema-first approach, allowing types and resolvers to be adjusted on-the-fly as new requirements emerge.
