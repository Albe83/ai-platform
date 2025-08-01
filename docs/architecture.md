# AI Platform Architecture

This document describes an AI Platform that exposes AI capabilities through a web interface, authenticates users via an OIDC provider, and routes requests through a gateway that abstracts external language models.

## Components

- **WebGUI**: User-facing interface built on OpenWebUI.
- **Identity Provider**: OIDC-compliant service (e.g., Microsoft Entra ID) that authenticates users for the WebGUI.
- **LLM Gateway**: Abstraction layer based on LiteLLM that routes requests to different model providers.
- **External Providers**: Managed or self-hosted large language models such as OpenAI, Anthropic, Gemini, or on-premise models like Mistral.

## Context Diagram

```mermaid
%%{init: { 'theme': 'neutral' } }%%
C4Context
    title AI Platform Context
    UpdateLayoutConfig("3", "1")

    Person(user, "User", "Interacts with the platform")
    System_Ext(idp, "Identity Provider", "Microsoft Entra ID")

    System_Boundary(platform, "AI Platform") {
        System(webgui, "WebGUI", "OpenWebUI")
        System(gateway, "LLM Gateway", "LiteLLM abstraction layer")
        System(mistral, "Mistral AI", "ollama")
    }

    System_Boundary(llms, "External LLMs") {
        System_Ext(openai, "OpenAI", "External LLM provider")
        System_Ext(anthropic, "Anthropic", "External LLM provider")
        System_Ext(gemini, "Gemini", "External LLM provider")
    }

    Rel(user, webgui, "Uses chat interface")
    Rel(user, idp, "Login via OIDC")
    Rel(webgui, idp, "Verify token signature")
    Rel(webgui, gateway, "Sends prompts for processing")
    Rel(gateway, mistral, "Forwards to local LLM")
    Rel(gateway, openai, "Forwards to external LLM")
    Rel(gateway, anthropic, "Forwards to external LLM")
    Rel(gateway, gemini, "Forwards to external LLM")
```

## Interaction Sequence

```mermaid
sequenceDiagram
    participant U as User
    participant W as WebGUI
    participant I as OIDC Provider
    participant G as LLM Gateway
    participant P as LLM Provider
    U->>W: Access platform
    W->>I: Redirect to login
    U->>I: Authenticate
    I-->>W: Return token
    U->>W: Submit prompt
    W->>G: Forward prompt
    G->>P: Request completion
    P-->>G: Return response
    G-->>W: Send response
    W-->>U: Display answer
```


