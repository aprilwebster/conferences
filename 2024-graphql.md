
# Implentation-First GraphQL
Speaker: Erik Wrede

- derive schema from the implementation
- ensure type safety
- for each typesript type, you get a GraphQL type
- typically referred to as code-first, but they want to rename it as implementation-first
   - differences?
- benefits
   - work with objects on your types as opposed to schema-first where root type might differ from resolver type?
 - root type vs child type
 - code-first is annotation based
 - implementation-first infers it? More type safe
 - single source of truth --
   - need structure in your code to hep with this
   - slim type definition and resolvers
   - system knows the connection between teh schema and implementation -- have tooling click to definition -- click to definition from client, through the schema and into the code
      - can add tooling

## Why Use it?
- leverage native language features
- production-ready
- 

## Frameworks
- leading frameworks: Strawberry, Hot Chocolate (annotation-based), Grats (typescript) (John Eldridge)

### [Strawberry](https://strawberry.rocks/)
- Around since 2018 or so with Python and have spent a of time on the DX
- Infers schema type based on schema annotation
- can exclude fields -- e.g., `Private`
- strawberry
   - Private
   - Scalars
   - Queries and Mutations are also just fields on object types
     
#### Native Generics
- e.g.,
-
T = TypeVar
Connection(Generic[T])

#### Field Extensions
- when you have some part of your schema that you want to autmomate away
- define mutation and input in two differnet locations - don't need to separate input type and mutation
- static contract ensure whenever have method, it ensures those fields are present.
- It does automatic conversion of fields into input types


## Approach
- Thinking impementation-first
- when working with data objects, already forms some sort of graph

### Best practics
- keep your resolvers thin (10 lines)
- check in your [SDL](https://www.apollographql.com/tutorials/lift-off-part1/03-schema-definition-language-sdl) -- to help people understand your schema


 
