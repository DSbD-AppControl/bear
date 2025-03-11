# BEAR Roadmap

This document outlines the planned development milestones for the **BEAR** (Behavioral Enforcement & Attestation Runtime) project. 

- **Context**: Modern software supply chains face significant integrity and confidentiality threats that are not fully addressed by traditional “linear” or solely pre-execution checks.  
- **Core Idea**: The framework applies **Multiparty Session Types (MPSTs)** to specify, enforce, and verify **application behavior**—including build pipelines and runtime systems—using both static and dynamic methods.  
- **Goal**: Provide a framework that supports *compositional reasoning* about trust boundaries (e.g., multiple build steps, different roles), enabling continuous attestation and verification throughout the software development lifecycle.

---

## Overview

### Phase 1: **Foundational Prototype**
1. **Minimum Viable Specification (MVS)**  
   - Use Scribble with *value-dependent refinements* to represent a simple build process as a *global protocol*.
   - Implement a proof-of-concept runtime monitor for an open source project. 
3. **Initial Documentation**  
   - Provide basic installation, usage instructions, and developer guidelines.
   - Publish a simple “Hello Build” tutorial illustrating an MPST-enforced build pipeline.

**Outcome**: Demonstrate how MPST-based behavioral checks can be integrated into a build/runtime environment, evaluate what other constructs/DSL features we need, and gather feedback from the community.

### Phase 2: **Core Feature Expansion**

1. **Refined Specification Language**  
   - Refine the specification language with any additional features we may need, based on Phase 1.
