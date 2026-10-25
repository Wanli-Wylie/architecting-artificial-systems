# The end-to-end argument

## The design and the question

Saltzer, Reed and Clark open with the claim that "Choosing the proper boundaries between functions is perhaps the primary activity of the computer system designer." Their paper concerns one such choice. A system includes a communication subsystem with a firm interface, and a list of functions (reliable delivery, duplicate suppression, ordering, acknowledgement, encryption) "might be implemented in any of several ways: by the communication subsystem, by its client, as a joint venture, or perhaps redundantly, each doing its own version." The case is about how that placement is reasoned. The argument "appeals to application requirements, and provides a rationale for moving function upward in a layered system, closer to the application that uses the function."

The subject is one design's placement of function rather than a governed system: a communication subsystem and its clients specified together or against a common interface. The authors note a pressure that makes the question real: "the communication subsystem is frequently specified before applications that use the subsystem are known", so the designer is "tempted to 'help' the users by taking on more function than necessary." The Internet is the later setting in which the placement became architecture. Its networks are separately administered, and Clark (1988) says that was a reason to join existing networks and not to design a unified one: "networks represent administrative boundaries of control". Those networks appear in this case as the environment the common interface has to accommodate.

## The argument

The argument runs as follows. A function that "can completely and correctly be implemented only with the knowledge and help of the application standing at the end points of the communication system" cannot be provided by the communication system alone, though "an incomplete version of the function provided by the communication system may be useful as a performance enhancement."

The worked example is careful file transfer between two hosts. Threats include faulty disk reads, copying mistakes in the programs, processor errors, a network that drops, alters or duplicates packets, and a host crash part way through. The alternative to reinforcing each step is an end-to-end check: the receiving part of the transfer program reads the stored copy back, recomputes a checksum, and returns it to the sender, which declares the transfer committed only if the two agree and otherwise retries. A reliable network removes one threat among five. If the application does the check anyway, the network's extra effort is "only reducing the frequency of retries by the file transfer application". It does not change whether the outcome is correct.

The paper reports a case from M.I.T. in which each hop between gateways had a packet checksum, and application programmers took the network to be reliable. A gateway, copying data between buffers, interchanged a byte pair about once in every million bytes, and source files of an operating system were corrupted, because "the transmitted data was unprotected while stored in each gateway." A check scoped to a hop covered the wire and not the gateway's own buffers, and the only check that spanned every step was the owners' "manual comparison with and correction from old listings."

The same reasoning is applied to delivery acknowledgement (what the application wants is an acknowledgement from the target application, "I did it", or "I didn't"), duplicate suppression (an application's own retries look like new messages to the network), FIFO ordering and encryption, where a network that encrypts must "be trusted to manage securely the required encryption keys".

## Copies below, for performance

Lower-level versions of a function are kept for performance, and the paper is explicit that correctness does not need them. On a network that loses one message in a hundred, whole-file retry grows exponentially costly with file length, so "some effort at the lower levels to improve network reliability can have a significant effect on application performance." The paper concludes that the effort is "an engineering tradeoff based on performance, rather than a requirement for correctness", and suggests providing "just the reliability that comes with little cost and engineering effort".

The paper also gives two reasons why a low-level copy can cost more than it seems: "those applications that do not need the function will pay for it anyway", and the lower level "may not have as much information as the higher levels." It does not settle where early checks go ("The end-to-end argument does not tell us where to put the early checks, since either layer can do this performance-enhancement job").

## The ends

The argument depends on what the ends are. For packet voice in a real-time conversation, low-level insistence on bit-perfect delivery adds uncontrolled delay, and a listener's "Would you please say that again?" covers dropouts. For voice stored for later listening, the recipient cannot ask for a repeat, so low-level accuracy helps. The strong version is "a property of the specific application – two people in real-time conversation – rather than a property, say, of speech in general", and the authors conclude that the argument "is not an absolute rule, but rather a guideline that helps in application and protocol design analysis". Clark makes the same observation as an engineering finding: for real-time speech "the most serious source of delay in networks is the mechanism to provide reliable delivery."

The paper names the opposing consideration. "A modularity argument prizes a reliable, FIFO sequenced, duplicate-suppressed stream of data as a system component that is easy to build on", and favours virtual circuits. The end-to-end argument says that centrally provided versions will be incomplete for some applications, which will find it easier to start from datagrams. The authors present end-to-end arguments as part of the answer to layerings built "without clearly defined criteria for assigning functions to layers."

## The Internet's interface and fate-sharing

Clark's account of the DARPA design shows the argument as built. The top-level goal was "an effective technique for multiplexed utilization of existing interconnected networks", and survivability, meaning communication continuing despite the loss of networks or gateways, was ranked first, with accountability last. IP offers the datagram, which "represents the minimum network service assumption": a packet of reasonable size, delivered "with reasonable but not perfect reliability", with addressing. Reliable or sequenced delivery, multicast, priority ranking and "internal knowledge of failures, speeds, or delays" are "explicitly not assumed". The contract is thin on purpose, and its failure outcomes (loss, reordering, duplication) are what the layers above are built to handle. Clark gives the benefit as range: the same datagram supports TCP's reliable stream, UDP for services such as the cross-Internet debugger and real-time speech, and networks as different as long-haul nets, local area nets, satellite and packet radio.

Clark gives a second reason for the same placement, which he calls fate-sharing. State about a conversation is kept in the hosts using it, so "it is acceptable to lose the state information associated with an entity if, at the same time, the entity itself is lost." The alternative, keeping the state in switches, would require replicating it, and fate-sharing "is much easier to engineer than replication" and protects against any number of intermediate failures. Gateways then become "stateless packet switches". Fate-sharing sets a boundary of lifetime: what dies with what. Clark states what it costs: "rather more trust is placed in the host", every host must implement the transport machinery, and "poor implementation of the mechanism may hurt the network as well as the host."

RFC 1958 (IAB, 1996) restates both in the later community's words: "the intelligence is end to end rather than hidden in the network", with state kept "only in the endpoints".

## Reading it in the vocabulary

The layering here is by interface. The application uses the communication subsystem through a contract, and it is not handed a task with latitude to be returned as a result, so delegation and a composition rule have nothing to say about it. The argument is a reason for where a layer's boundary falls: a function belongs where the requirement and the knowledge needed to complete and verify it coincide, which is the application, and a copy below is justified by cost. The contract is thin and states failure, so what the application assumes of the layer below is exactly what the contract admits, and it checks the rest itself. That is how the argument reformulates the question. "How reliable should the network be?" becomes "who can establish that the function was done?", and the answer to the second is the same whatever is chosen for the first, leaving the first as a question about performance.

Boundaries in the case change ownership of function, trust (what the hosts must be trusted with) and lifetime (fate-sharing). The requirements are the application's and are met at the end, apart from the lower layer's own performance qualities.

## Where the vocabulary strains

The sources say "end points", "hosts", "entities", "the application" and "the network". "Source of truth" does not fit fate-sharing, which concerns where state lives and what it survives, not which copy wins in a disagreement. Saltzer et al. write "low levels" and "lower level" and Clark and the RFC write "layer"; the case quotes each as its source's, and the interface-defined steps here are layers in the vocabulary's sense. The paper's "guideline" is the weight the authors give their own argument, and the case reports it so.

## Sources

- J. H. Saltzer, D. P. Reed and D. D. Clark, "End-to-End Arguments in System Design," ACM Transactions on Computer Systems 2(4), November 1984, pp. 277-288 (revised from the 1981 ICDCS paper); MIT-hosted copy at web.mit.edu/Saltzer/www/publications/endtoend/endtoend.pdf.
- D. D. Clark, "The Design Philosophy of the DARPA Internet Protocols," Proc. SIGCOMM '88, Computer Communication Review 18(4), August 1988, pp. 106-114.
- B. Carpenter (ed.), IAB, RFC 1958, "Architectural Principles of the Internet," June 1996.
