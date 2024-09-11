
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

# LLM
Graph schema is in the LLM -- can easily understand GraphQL
GraphQL is better for GI
Just need to be worried about writing the query

Can we orifuce a graphQL contet
- using RAG
  takebreak apart the schema and create vector rep using some embedding model (openAPI or llama) to take text and turn into model
  cvector search to get relevant parts of document

HOw do you do this?
- very simple
- DEMO

Github schema: github.graphql
- github really good at commenting
- ADD COMMENTS IN GRAPHQL SCHEMA - semantics for pieces of schema, very helpful for LLMs
- add a lot of metadata and even tha arguments, add as much verbosity to arguments; opportunities for us to change that
- decisions in how you make decisions
- Garner - 30% of traffic from LLMs and AI - one of clients need to support in the future
- with graphql already there

Step 1: create embedded rep
- read schema and parse i, take definitions and create a rep of the string object

### Tools
ollama
openai, gemini
token counting -- see a lot in the openapi space -- for pricing
npm scripts tab in VSCbree
break graphql scheme into definitions (but could use fields) and vectorize
does vector search (top k relevant -- it's the retriever in th code in `generate.js`)
has prompt for langchain -- `docPrompt`

docs get added to context that is then sent to LLM

ideal version of github v5 -- text box at top
 mongo db for vector store
 bring AI into API strategy
 first question -- use it with internal developers first, then put in front of customers -- then have more confidence


 YELP schema -- two parts, one is plural version of word, the way it gets nested so the LLM gets confused and have hallucinations. LOok at confidence store of documents!
 - Mongo API makes it easy to get confidence for each document
 - definitely an aspect of schema design
 - root level of query in journey to create operation -- richness of that, product entry point to triage into various capabilities of products -- what are tht things you can do with the product and different fector searches
 - vectorize into different vectorizaion for two sets of docs -- definitions, then secon is fields types
 
