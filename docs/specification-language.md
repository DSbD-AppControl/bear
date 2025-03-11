# BEAR Specification Language

We propose to define a specification language by extending Scribble, a language initially developed to encode specifications of communications protocols, based on the theory of **Multiparty Session Types**. A particular advantage of MPSTs is that they are **composable**. This allows us to focus in on an arbitrarily granular subsets of application behaviour and incrementally introduce security measures, with minimal disruption to other parts of the system.

The specification language can be used in a **top-down** or **bottom-up** fashion. 

* The **top-down** would be to describe the *build process* as a *global protocol*. This would give a comprehensive view of all information exchanged between *build steps*, thus allowing us to check artefacts and provenance information at multiple points in time during the build.

* The **bottom-up** approach would be to describe individual *build steps* through their *local types*, implement the required enforcement mechanisms and thereafter check for compatibility whenever two build steps communicate. 

## Multiparty Session Types

We will base our specification language on **Multiparty Session Types**, which are a formalism used to model and verify communication protocols involving multiple participants in a concurrent system. Adapting this formalism for use with build systems requires nothing more than to view information exchange between build steps through the lens of communication.

In MPST terminology, a **global protocol** is a top-down description of the **sequencing** and **structure** of **messages** exchanged between **participants**. For our purposes, we can recast these notions into build system terms as follows:

- The **global protocol** is a **behavioural specification** for the entire **build process**.
- **Participants** correspond to individual **build steps** in the process.
- **Messages** correspond to build step **inputs** and **outputs**, including but not limited to: artefacts, provenance information, and parameters.

### Projection

The global protocol can be **projected** onto a set of corresponding **local types**, one for each participant. Local types describe communication from the point of view of a participant. This projection operation is said to preserve the protocol, meaning that, if participants adhere to their local types, then communication mismatch and deadlock scenarios cannot occur.


### Compatibility

In MPSTs, message exchanges between participants are always **typed** and checked for **compatibility**. That is to say, if at any point in time *Participant A* sends a message *m* having a type *T* to *Participant B*, compatibility ensures that *Participant B* will receive a message of type *T*. In the *Scribble* language, MPST participants are represented abstractly as **roles**. The following *Scribble* example shows a global protocol in which a message with type **program** is sent from a participant assuming the **Client** role to the participant assuming the **BuildServer** role.

```scribble
protocol Build(role Client, role BuildServer) {
    BuildStep(program) from Client to BuildServer;
    choice at BuildServer {
        accept() from BuildServer to Client;
    } or {
        reject() from BuildServer to Client;
    }
}
```

Compatibility ensures not only the correctness of individual message types but also the consistency of entire sequences of messages in every transaction. In the Scribble example above, the BuildServer role has static knowledge of the type of request it can receive from the Client. Similarly, the Client role is guaranteed to receive either an accept or reject message as a reply. This guarantees that each role or participant can independently verify the behavior of its counterparts.


### Value Dependence

Multiparty Session Types come in many different flavors. **Refined MPSTs** are a particular extension of Multiparty Session Types that can express the relationship or dependence between a message's value and the behavioral type describing subsequent communication. In the following example snippet, a Client contacts a Build Server with a compile request. The **Request** message comes with a **refinement**, a predicate that must evaluate to true for the message to be considered valid, which captures the essence of a `%.o: %.c` rule in Makefiles.

```scribble
protocol Build (role Client, role Server) {
    Request(
        sourceFile: string { hasSuffix(sourceFile, ".c") }
        , targetFile: string { hasSuffix(targetFile, ".o") 
            && matchesBaseName(sourceFile, targetFile) }
    ) from Client to BuildServer;    
}
```

Value dependence is useful because it allows for a more expressive specification language, one that is capable of describing and reasoning about application behavior that is conditional on run-time values. Continuing where we left off with the example protocol snippet above, we see that refinements can also refer to values from previous messages:

```scribble
    choice at Server {
        Success( producedFile: string { targetFile == producedFile }) from Server to Client;
    } or { 
        Failure(errorMessage: string) from Server to Client; 
    }
}
```

When the build server is done compiling, it replies to the Client. It must necessarily do so by returning either a **Success** or **Failure** message. The refinements included in the example above ensure that **Success** messages always contain the name of the compiled output file and that this file matches the **targetFile** specified by the Client in its request.
