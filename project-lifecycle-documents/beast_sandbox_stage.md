## Application for creating a new project at Sandbox stage

### List of project maintainers

*  Cristian Urlea, University of Glasgow, @CristianUrlea
*  Laura Voinea, University of Glasgow, @LauraVoinea
*  Wim Vanderbauwhede, University of Glasgow, @WimVanderbauwhede
*  Martin Vassor, Université de Lorraine and Loria, @Bromind


### Mission and Alignment

The project must be aligned with the OpenSSF mission and either be a novel approach for existing areas, address an unfulfilled need, or be initial code needed for OpenSSF WG work. It is preferred that extensions of existing OpenSSF projects collaborate with the existing project rather than seek a new project.

> The mission of the project is to develop the Behavioural Enforcement and
> Attestation Runtime aimed at securing open-source software by enabling
> security automation throughout the software development lifecycle. This framework will
> leverage formal specification languages, static analysis techniques, and
> runtime monitoring and enforcement to ensure robust security postures. By 
> integrating these components, the framework will provide a comprehensive solution
> for specifying, verifying, and enforcing the expected behaviour of software
> applications, thereby reducing the risk of vulnerabilities and attacks.

Our project directly aligns with the OpenSSF mission. By developing a formal specification language for application behaviour we enable a higher degree of automation in developing, maintaining and consuming secure open source software. This approach builds upon the practice of behaviour-driven development (BDD), enabling automated reasoning about software behaviour. 

> The Open Source Security Foundation (OpenSSF) seeks to make it easier to sustainably secure the development, maintenance, and consumption of the open source software (OSS) we all depend on. This includes fostering collaboration, establishing best practices, and developing innovative solutions.

#### Specific Goals Include:

*  Formal Specification Language: Develop a language based on Multiparty Session Types (MPSTs) to formally specify application behaviour.
*  Compositional Security: Enable compositional reasoning about application behaviour before, during, and after execution
*  Static and Dynamic Verification: Enable the development of tools for both static and dynamic verification of security properties.
*  Enhanced Supply Chain Security: Improve the security of software supply chains by verifying and enforcing the behaviour of build processes
and software artefacts.
*  Compatibility Checking: Ensure compatibility between applications and their dependencies, through behavioural specifications.
*  Runtime Monitoring and Enforcement: Implement mechanisms to monitor and enforce specified behaviours at runtime.
*  Observational Reproducibility: Introduce the concept of observationally reproducible builds to ensure that build processes and artefacts are observationally equivalent
*  Integration with Existing Tools: Complement and integrate with existing tools and standards such as SLSA, Witness, and SPIFFE.

### Project References

| Reference                              | URL                                                                                                  |
|----------------------------------------|------------------------------------------------------------------------------------------------------|
| Repo                                   | https://github.com/DSbD-AppControl/bear                                                             |
| Contributing guide                     | https://github.com/DSbD-AppControl/bear/blob/main/CONTRIBUTING.md                                   |
| Roadmap                                | https://github.com/DSbD-AppControl/bear/blob/main/docs/roadmap.md                                   |