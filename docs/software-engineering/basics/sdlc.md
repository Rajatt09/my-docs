# Software Development Life Cycle (SDLC)

## What is SDLC?

The Software Development Life Cycle (SDLC) is a systematic process for building software applications that ensures their quality and correctness. The SDLC process aims to produce high-quality software that meets customer expectations and completes development within time and cost estimates.

```mermaid
graph TD
    A[Planning] -->|Requirements Gathered| B[Analysis]
    B -->|Requirements Defined| C[Design]
    C -->|Architecture Created| D[Implementation]
    D -->|Code Developed| E[Testing]
    E -->|Software Verified| F[Deployment]
    F -->|Live Release| G[Maintenance]
    G -->|Updates Required| A
```

## Key Objectives

- Deliver high-quality software
- Meet customer expectations
- Complete within timeline and budget
- Follow best practices and standards

## SDLC Stages

## 1. Planning and Requirement Analysis

```mermaid
flowchart TD
    A[Gather Requirements] --> B[Analyze Requirements]
    B --> C[Document Requirements]
    C --> D[Validate Requirements]
    D --> E[Create Project Plan]
```

## 2. Defining Requirements

```mermaid
flowchart LR
    A[Business Requirements] --> B[Technical Requirements]
    B --> C[Functional Requirements]
    C --> D[Non-Functional Requirements]
    D --> E[SRS Document]
```

- This is fulfilled by utilizing SRS (Software Requirement Specification). This is a sort of document that specifies all those things that need to be defined and created during the entire project cycle.

## 3. System Design

### Two approaches to System Design:

1. **Top-Down Approach** (High Level → Low Level)

   - Start with overall system architecture
   - Break down into smaller components
   - Good for understanding big picture first

2. **Bottom-Up Approach** (Low Level → High Level)
   - Start with detailed components
   - Combine into larger systems
   - Good for understanding implementation details first

### Design Hierarchy:

```mermaid
graph TD
   A[Requirements Analysis] --> B[Low Level Design]
        B --> C[High Level Design]
        C --> D[System Architecture]
```

```mermaid
graph TD
    subgraph "System Design"

        subgraph "Low Level Design"
            B1[Class Design]
            B2[Algorithm Details]
            B3[Data Structures]
        end

        subgraph "High Level Design"
            C1[Component Design]
            C2[Interface Design]
            C3[Database Design]
        end

        subgraph "System Architecture"
            D1[Overall Structure]
            D2[System Integration]
            D3[Deployment Plan]
        end
    end
```

- SRS is a reference for software designers to come up with the best architecture for the software. Hence, with the requirements defined in SRS, multiple designs for the product architecture are present in the Design Document Specification (DDS).

## 4. Implementation

- At this stage, the fundamental development of the product starts. For this, developers use a specific programming code as per the design in the DDS.
- Programming tools like compilers, interpreters, debuggers, etc. and languages like C/C++, Python, Java etc. are also put into use at this stage.

```mermaid
flowchart LR
    A[Code Development] --> B[Code Review]
    B --> C[Unit Testing]
    C --> D[Integration]
```

## 5. Testing and Integration

```mermaid
flowchart TD
    A[Unit Testing] --> B[Integration Testing]
    B --> C[System Testing]
    C --> D[Acceptance Testing]
    D --> E[Performance Testing]
```

## 6. Deployment

```mermaid
flowchart LR
    A[Build Release] --> B[Deploy to Staging]
    B --> C[User Acceptance]
    C --> D[Production Deployment]
```

## 7. Maintenance

```mermaid
flowchart TD
    A[Monitor System] --> B[Bug Fixes]
    B --> C[Updates]
    C --> D[Enhancements]
    D --> A
```

Reference: [Click here](https://www.geeksforgeeks.org/sdlc-models-types-phases-use/?ref=lbp)
