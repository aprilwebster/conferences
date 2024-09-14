# Conference: GraphQL 2024
I attended one day of the 2024 SF GraphQL Conference. I got a pass by reaching out to the CTO of IBM Software (founder of 

- **Location**: San Francisco
- **Dates**: Sept 10-12, 2024
- **Schedule**: https://graphql.org/conf/2024/
- **Notes**: this conference doesn't have any volunteer opportunities nor diversity scholarships

# Talks 
I attended the following talks:

### [Why You Should Use Implementation-First to Build Your GraphQL Schema (Erik Wrede, fulfillmenttools, Software Engineer)](https://graphql.org/conf/2024/schedule/c13801cab4bdcf1c9e7321fba8daca3f/?name=Why%20You%20Should%20Use%20Implementation-First%20to%20Build%20Your%20GraphQL%20Schema)

#### Overview
- Speaker: Erik Wrede ([LinkedIn](https://www.linkedin.com/in/erikwrede/))
- [Slides](<Implementation-First-GraphQL Conf 2024.pdf>)
- Video

#### Abstract
When we look at GraphQL server implementation approaches, you often see the discussion between code-first and schema-first as a schema building approach. What is overlooked is that Facebook actually built their Hack-based GraphQL server with implementation-first. This approach will infer the GraphQL schema from your code, and by extension from your business layer. In this talk, I will look at various implementations of implementation-first and explain why Facebook chose this approach to build their own GraphQL server and why it is actually the better approach in most projects.


### [Dynamically Serving a GraphQL API with Custom Types at Runtime (Emily Li, Benchling, Software Engineer)](https://graphql.org/conf/2024/schedule/24100908c07eed48ee464ca2509ef527/?name=Dynamically%20Serving%20a%20GraphQL%20API%20with%20Custom%20Types%20at%20Runtime)

#### Overview
- Speaker: 
- Slides
- Video

#### Abstract
Existing GraphQL frameworks are well designed to handle statically defined types and resolvers. Here at Benchling, we faced the problem of serving a GraphQL API which incorporated customer-defined types at runtime with a dynamically generated graph that varies customer-to-customer. In this talk, I’ll describe some of the challenges in serving this GraphQL API, including dynamic generation of graph components and performance. Then, I’ll describe how we extended Strawberry (the GraphQL framework we decided to use) to handle our use cases as well as a graph-caching strategy that allowed us to dramatically improve the performance of serving the API.

### [Dynamic (but Safe) Operations: Using AI to Generate Trusted Operations from Text Prompts (Michael Watson, Apollo GraphQL, Developer Relations Manager)](https://graphql.org/conf/2024/schedule/f02cda18e19887fddeb56b06445ac256/?name=Dynamic%20(but%20Safe)%20Operations%3A%20Using%20AI%20to%20Generate%20Trusted%20Operations%20from%20Text%20Prompts)

#### Overview
- Speaker: 
- Slides
- Video

#### Abstract
Platform engineering and internal developer portals have been a growing trend in the tech industry to make developers more efficient. For example, how do we help new developers ship their first feature faster? GraphQL helps Platform API efforts ship features faster, but what about when your schema gets very complex? How can a new developer find what they need quickly? GraphQL already provides a complete and understandable description of the data in our APIs, but what if we provide that context to a LLM? In this talk, we'll journey through GitHub's APIs and explore how a GraphQL schema is a significant advantage in AI-based tooling. We're seeing more AI-based tools generate fetch code based on OpenAPI definitions, and while they may be tempting at first, it could be a decision with unexpected trade-offs. We'll show how to take a standard open-sourced LLM and provide a GraphQL-aware context to generate operations from text input. After this talk, you can safely bring AI to your developer efficiency initiatives with any LLM, 3rd party, or self-hosted!




## Overview 
## Networking
Check out the docs
http://strawberry.rocks
http://grats.capt.dev
You can find me on

## Resources


## Talk Notes
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

use deprecared
too many repeatable thigs -- docs have overlap

Comments metadata ideas -- USE LINTING
Governance control for 
inting rules -- that requires a comment especially for a platform API -- require minimum bill of materials, auth pattern, headers, what you contribute

GOVERNANCE -- process, support beck end for front end, those who create APIs want to have ownership and maybe not have as much desire to support others in org
some teams support many teams and wantto 
follow as cosely where are to meet developers and fows where they are -- wrap the governance where they are

EXPORERE in graphql -- copy operation to graphQL\

# Security
- disable introspection in production
   - exposes how your schema is constructed -- malicious attacks, payloads, etc
   - it's only okay for PUBLIC APIS, ot internal
   - use automatic tools
- robust authentication
   - How to do this
      - use secure protocols
      - impement rstrong autheication (Jwt, Oauth)
      - validate tokens for every request
      - securely manage sessions
      - enforce password policies
      - offer multi-factor auth
      - example
         - 23 and me -- brute force attack as login API endpoint wasn't enforcing authenication
- Limit Query Depths
      - can lead to performance degradation, DOS attacks, resource exhaustion, increased operational costs
- Use persisted queries
  - document allow-list -- persisted queries or stored operations
     - whitelists your queries
     - backend checks if allow list
     - very popular way to prevent malicious attacks
  - API security implications -- shifts security to development phase (easier to check), but adds burden to developers to maintain these
- Input Validation
   - protects agains injection attacks, XSS
 - Secure Direct Object References
   - implement auth checks in a resolver function to secure direct object references in GraphQL
   - if not exposes sensitive data to unauthorized users
- Error Handling
   - create afunction to parse and handle errors in your application don't expose any sensitive data. Don't have verbose info. e.g., Connt query field email on X.
- Query Complexity Analysis
   - how complex is your query -- is at risk for DoS attacks
   - implement query complexity analysis middleware -- assign scores to it and then limit queries of score that's too high
- Mass Assignment Checks
   - not very common, but critical
   - able to edit a parameter in a mass way which isn't allowed (e.g., API takes form input and the user is also able to add a parameter they aren't allowed to add but API doesn't check) -- this makes the user an ADMIN
- Excessive Data Exposure
   - implement a field-level auth check in the resolver to avoid account takeover
