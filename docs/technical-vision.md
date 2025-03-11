# BEAR Technical Vision 

## Introduction 

This document presents a case for the development of a **Behavioural Enforcement and Attestation Runtime** to secure open-source software for the greater public good by enabling security automation at all stages of the software development lifecycle. Through this, we propose to develop a specification language based on Multiparty Session Type Theory and Capability-based security concepts, and a set of tools integrating the specification language, static analysis techniques and run-time monitoring and enforcement.

 The framework is designed to support a more robust security posture by allowing for compositional reasoning about, and monitoring/enforcement of, application behaviour before, during and after execution


## Motivation

Supply chain vulnerabilities and attacks pose significant risks globally, resulting in lost revenue, mitigation expenses, disruption of critical services, and diminished trust. Current efforts aimed at securing against supply chain vulnerabilities primarily tackle the issue by providing the means to **attest** to and **verify** the **authenticity** and **integrity** of software packages as produced by **trusted build platforms**.


## Problem Statement

Many efforts aimed at securing software supply chains are narrowly focused on the issue of artefact integrity and place a large amount of trust in the build platforms that produce them. Unconditional trust in the build platform, and relying solely on pre-execution provenance checks, overlooks important threats, particularly those related to **confidentiality**. Similarly, there are other simplifying assumptions and design decisions commonly adopted, perhaps out of the practical necessity of enabling incremental adoption, that are detrimental to security in the long-run.

### Coarse Granularity

The first issue with existing approaches is that trust boundaries are defined too broadly. For instance, the **Supply Chain Levels for Software Artifacts (SLSA)** specification identifies three general trust domains: one for the **Build Environment**, another for the **Control Plane**, and a third encompassing **everything else**.

Unfortunately, this leaves a large window of opportunity in which malicious actors can exfiltrate sensitive information from the build platform, tamper with attestation information before it is signed, and generally influence subsequent build steps.

### Linear Structure

The second issue is that, while modeling software builds as **linear sequences of steps** makes reasoning about the integrity checking process easier, it can also lead to loosing track of important details. Some build steps, such as executing a suite of tests, can be **conditional** on the type of build (e.g. debug or release). Likewise, the output from different build steps can have varying degrees of impact on subsequent steps. The outcome of running the test suite might, for example, determine whether or not the **package** step is executed. Yet, output from the **test** phase (e.g., test suite execution logs) is only communicated to the **sign** and **execute** steps, skipping **package**.

 ## Approach

Our first priority will be to develop an appropriate [**specification language**](./specification-language.md) capable of representing application behaviour in a manner that is useful for reasoning about the security properties of all types of applications, particularly build processes. For this purpose, we propose to extend the **Scribble** language, based on the theory of **Multiparty Session Types** (MPST).

Once a sufficiently expressive specification language is defined, our next priority will be to develop the means to **verify** and **enforce** application behaviour. For this purpose, we will describe a number of use-cases related to build systems and supply chain integrity. It is worth mentioning that many of the use-cases could be implemented by directly targeting or minimally extending existing tools and technologies such as Witness, Spiffe/Spire, gittuf, and others.
