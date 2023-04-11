# BSY

## Topics
Security analysis of operating systems, development of secure software and web applications security. Analysis of cyberattacks and malware. Security of mobile devices.
BE4M36BSY (Course web pages)

## Questions
### Managing a software project with a security as an objective advantages and disadvantages of waterfall and ellipse model for this use-case
1. **Secure by Design**:
   - Integrate security best practices from the start
   - Follow secure coding standards and guidelines
   - Use secure frameworks and libraries

2. **Security Training**:
   - Educate developers on secure coding practices
   - Conduct regular security training and awareness sessions

3. **Threat Modeling**:
   - Identify and analyze potential threats and vulnerabilities
   - Develop strategies to mitigate or eliminate risks

4. **Secure Development Lifecycle (SDLC)**:
   - Incorporate security into each phase of the development process
   - Use a security-focused approach like Microsoft's Security Development Lifecycle (SDL)

5. **Automated Security Testing**:
   - Implement tools to perform static and dynamic security testing
   - Continuously scan code for vulnerabilities and security flaws

6. **Code Review and Auditing**:
   - Conduct manual code reviews to identify security issues
   - Employ external security audits for unbiased evaluation

7. **Patching and Maintenance**:
   - Regularly update and patch dependencies, libraries, and frameworks
   - Monitor security advisories and apply security updates promptly

8. **Incident Response and Recovery**:
   - Establish an incident response plan
   - Learn from incidents and improve security measures

**Waterfall Model**

Advantages:
- Easy to understand and implement
- Clear structure with well-defined stages
- Simple to manage due to sequential nature
- Emphasizes documentation and design upfront

Disadvantages:
- Inflexible, not suitable for projects with changing requirements
- Limited opportunity to incorporate security feedback from later stages
- Difficult to identify security issues until late in the process
- Prolonged time to market, delaying security updates or patches

**Spiral Model**

Advantages:
- Iterative and flexible, allowing for evolving security requirements
- Encourages risk assessment and threat modeling early in the process
- Facilitates continuous security improvements with each iteration
- Enables frequent testing and validation of security measures

Disadvantages:
- More complex and difficult to manage compared to Waterfall
- Requires experienced project managers and security experts
- Can be costly and time-consuming due to iterative approach
- Risk of scope creep or deviation from initial security objectives
  
### Systematic identification of potential vulnerabilities

1. **Asset Inventory**:
   - List and categorize all assets (hardware, software, data)
   - Understand the value and sensitivity of each asset

2. **Threat Modeling**:
   - Identify threats relevant to your organization or industry
   - Analyze potential attack vectors and impacts

3. **Vulnerability Scanning**:
   - Use automated tools to scan for known vulnerabilities
   - Regularly update and perform scans across your infrastructure

4. **Penetration Testing**:
   - Simulate real-world attacks to test defenses
   - Employ internal or external teams to perform testing

5. **Code Review and Auditing**:
   - Conduct manual code reviews to identify security issues
   - Employ external security audits for unbiased evaluation

6. **Security Assessments**:
   - Perform regular security assessments on systems and processes
   - Evaluate the effectiveness of security controls and policies

7. **Security Information and Event Management (SIEM)**:
   - Monitor and analyze logs, events, and alerts
   - Identify anomalies and signs of compromise

8. **Incident Response and Recovery**:
   - Establish an incident response plan
   - Learn from incidents and improve security measures

9. **Security Training and Awareness**:
   - Educate employees on security best practices
   - Conduct regular training and awareness sessions

10. **Information Sharing and Collaboration**:
   - Participate in industry and community security initiatives
   - Share threat intelligence and learn from others' experiences

### STRIDE
- *Definition*: A threat modeling methodology developed by Microsoft to systematically identify potential threats in a system or application
- *Acronym*: Each letter represents a category of threats

1. **S - Spoofing**:
   - Impersonating a legitimate user, process, or system
   - Examples: phishing, fake websites, forged email headers
   - Mitigation: Authentication mechanisms, digital signatures, certificate validation

2. **T - Tampering**:
   - Unauthorized modification of data or system components
   - Examples: Man-in-the-middle attacks, unauthorized code changes
   - Mitigation: Data integrity checks, encryption, secure coding practices, input validation

3. **R - Repudiation**:
   - Denying having performed an action or the ability to prove an action occurred
   - Examples: Disputing a financial transaction, removing traces of unauthorized actions
   - Mitigation: Audit trails, logging, digital signatures, non-repudiation mechanisms

4. **I - Information Disclosure**:
   - Unauthorized access or disclosure of sensitive information
   - Examples: Data leaks, unauthorized access to database, information leakage through side channels
   - Mitigation: Encryption, access controls, secure communication channels, data classification

5. **D - Denial of Service (DoS)**:
   - Disrupting the availability or functionality of a system or service
   - Examples: DDoS attacks, resource exhaustion, system crashes
   - Mitigation: Load balancing, traffic filtering, rate limiting, secure coding practices

6. **E - Elevation of Privilege**:
   - Exploiting vulnerabilities to gain unauthorized access or privileges
   - Examples: Privilege escalation, bypassing access controls, exploiting software flaws
   - Mitigation: Principle of least privilege, secure coding practices, regular patching and updates

### Attack modelling (attack trees)
- *Definition*: A graphical, hierarchical method for systematically analyzing and representing potential attacks on a system or application
- *Purpose*: To identify, evaluate, and prioritize threats, and to develop strategies to mitigate or eliminate them

**Key Components**:

1. **Root Node**: Represents the primary goal or objective of the attacker
2. **Intermediate Nodes**: Represent sub-goals or intermediate steps to achieve the root node objective
3. **Leaf Nodes**: Represent the specific attack techniques or actions needed to achieve the parent node's sub-goal

**Attack Tree Creation Process**:

1. **Identify the Objective**: Define the primary goal of the attacker (e.g., gain unauthorized access, disrupt service)
2. **Brainstorm Sub-Goals**: Break down the primary goal into smaller sub-goals or steps
3. **Define Attack Techniques**: List specific techniques or actions that could be used to achieve each sub-goal
4. **Organize Hierarchically**: Arrange the sub-goals and attack techniques into a tree structure, with the primary goal as the root node and specific attack techniques as leaf nodes
5. **Analyze and Prioritize**: Assess the likelihood, impact, and difficulty of each attack technique or path, and prioritize threats accordingly
6. **Develop Mitigation Strategies**: Identify security controls or countermeasures to address the identified threats

**Benefits of Attack Trees**:

- Systematic and structured approach to threat modeling
- Facilitates clear communication and understanding of potential threats among stakeholders
- Enables identification of common attack paths and shared mitigation strategies
- Supports quantitative or qualitative analysis of threats
- Provides a basis for prioritizing security investments and efforts

### Ranking of vulnerabilities (ideal, DREAD)

- *Purpose*: To prioritize vulnerabilities based on their potential impact, likelihood, and severity, in order to allocate resources and efforts effectively

**Ideal Approach**:

1. **Impact Assessment**: Evaluate the potential harm a vulnerability could cause if exploited
2. **Likelihood Assessment**: Estimate the probability that a vulnerability will be exploited
3. **Severity Assessment**: Combine impact and likelihood assessments to determine the overall severity of a vulnerability
4. **Prioritization**: Rank vulnerabilities based on their severity and allocate resources accordingly
5. **Mitigation**: Implement security controls or countermeasures to address the highest priority vulnerabilities first

**DREAD Model**:

- *Definition*: A qualitative risk assessment model used to rank and prioritize vulnerabilities
- *Acronym*: Each letter represents a factor to consider when assessing a vulnerability's risk

1. **D - Damage Potential**: Assess the potential harm that could be caused by exploiting the vulnerability
2. **R - Reproducibility**: Evaluate how consistently the vulnerability can be exploited
3. **E - Exploitability**: Estimate the difficulty or complexity of exploiting the vulnerability
4. **A - Affected Users**: Determine the number of users or systems that could be impacted by the vulnerability
5. **D - Discoverability**: Assess the likelihood that the vulnerability will be discovered by an attacker

**DREAD Process**:

1. Rate each DREAD factor on a predefined scale (e.g., 1-10)
2. Calculate the average score across all factors for each vulnerability
3. Rank vulnerabilities based on their average DREAD score
4. Prioritize mitigation efforts according to the ranked vulnerabilities

Keep in mind that the DREAD model is just one approach to vulnerability ranking. Organizations may choose to use other models or develop their own customized approaches based on their specific needs and priorities.

While the DREAD model has been widely used for vulnerability risk assessment, it is not considered ideal for several reasons:

1. **Subjectivity**: The DREAD model relies on subjective judgments when rating each factor, which can lead to inconsistencies and inaccuracies in the risk assessment. The lack of clear definitions and guidelines for each factor can further contribute to this subjectivity.
2. **Lack of Granularity**: The DREAD model's simple 1-10 rating scale may not provide enough granularity to distinguish between different levels of risk accurately. This can make it challenging to prioritize vulnerabilities effectively.
3. **Incomplete Factors**: The DREAD model does not cover all relevant aspects of a vulnerability's risk. For example, it does not consider factors like the existing security controls, the vulnerability's age, or the potential financial impact of a successful exploit.
4. **Arithmetic Mean**: The DREAD model uses the arithmetic mean to calculate the average risk score. This approach may not accurately reflect the overall risk, as it assumes that all factors are equally important. In reality, certain factors may have a more significant impact on the overall risk than others.
5. **Static Scoring**: The DREAD model does not account for the evolving nature of threats and vulnerabilities. The risk scores may not reflect the current state of the threat landscape or the effectiveness of new security measures.

These limitations have led to the development of alternative risk assessment models and methodologies, such as the Common Vulnerability Scoring System (CVSS), which provides a more comprehensive and objective framework for assessing and prioritizing vulnerabilities.

### Timing and storage covert channels

**Timing Covert Channels**:
- *Definition*: Exploit timing of events or processes for secret communication
- *Encoding*: Sender and receiver agree on time-based encoding
- *Examples*:
  1. **Inter-packet delays**: Manipulate time intervals between network packets
  2. **CPU usage**: Vary usage to create encoding pattern
  3. **Response time**: Influence service or resource response time
- *Mitigation techniques*:
  1. Traffic shaping
  2. Regularizing event timings
  3. Monitoring unusual timing patterns

**Storage Covert Channels**:
- *Definition*: Use shared storage resources to encode/transfer info secretly
- *Encoding*: Sender alters shared resource, receiver observes changes
- *Examples*:
  1. **File content or metadata**: Modify shared file's content or metadata
  2. **Shared memory**: Write/read data in specific memory location
  3. **Database records**: Manipulate shared records or tables
- *Mitigation techniques*:
  1. Access control and monitoring
  2. Regular audits of shared resources
  3. Anomaly detection and data integrity checks

### Side channel attacks
- *Definition*: Exploit unintentional information leakage from a system to break security or encryption
- *Information Sources*: Physical characteristics or implementation details
- *Examples*:
  1. **Timing attacks**: Analyze time taken to perform cryptographic operations
  2. **Power analysis attacks**: Monitor power consumption patterns
  3. **Electromagnetic attacks**: Capture emitted electromagnetic signals
  4. **Acoustic attacks**: Record sounds produced by a system's components
  5. **Cache attacks**: Exploit access patterns of shared memory caches
- *Targets*: Cryptographic systems, secure hardware, secure communication channels
- *Mitigation techniques*:
  1. Constant-time implementations
  2. Randomizing execution time or power consumption
  3. Shielding or isolation of sensitive components
  4. Noise generation to mask true signals
  5. Regular security audits and updates
### Steganography
- *Definition*: Concealing information within other non-secret data or media
- *Goal*: Hide existence of secret communication, unlike cryptography which focuses on protecting content
- *Common Techniques*:
  1. **Image steganography**: Embed secret data within image pixels, colors, or formats
  2. **Audio steganography**: Hide data in audio files using frequencies, amplitudes, or noise
  3. **Text steganography**: Conceal information within text using spaces, characters, or formatting
  4. **Video steganography**: Encode data within video frames or compression artifacts
  5. **Network steganography**: Use network protocols, headers, or packet timing to hide data
- *Detection*: Steganalysis techniques, statistical analysis, or machine learning algorithms
- *Uses*: Secure communication, watermarking, covert channels, espionage
- *Mitigation techniques*:
  1. Access control and monitoring
  2. Regular audits of data and media
  3. Anomaly detection and content filtering
  4. Employee training and awareness

### Discretionary access control(Access control list, Capabilities)
**Discretionary Access Control (DAC)**:

- *Definition*: Access control model where resource owners decide access permissions for other users
- *Key Features*: Flexibility, user-driven access management, based on user identity and/or group membership
- *Potential Risks*: Information leakage, unauthorized access, dependency on user's discretion

**Access Control List (ACL)**:

- *Definition*: List of access permissions attached to a resource, specifying which users or groups can perform actions
- *Components*: Resource, user/group, action (e.g., read, write, execute), access rule (allow/deny)
- *Implementation*: File systems, databases, network devices
- *Benefits*: Fine-grained control, ease of management, explicit permissions
- *Challenges*: Scalability, complexity, maintaining consistency

**Capabilities**:

- *Definition*: Token-based system where users possess tokens that grant them access to specific resources or actions
- *Components*: Token (represents access right), resource, action
- *Implementation*: Object-oriented systems, some operating systems, microkernel architecture
- *Benefits*: Fine-grained control, decentralized management, reduced risk of unauthorized access
- *Challenges*: Token management, token revocation, token forgery protection

### Mandatory access control

### Multi-level security

### Biba model

### Multi-lateral security

### Role-based access control

### Privilege escalation, security of operating systems, trusted computer base, reference monitor, complete mediation, needed mechanism for securing current OS, memory management, rings.

### Virtualization, virtual machine monitor, micro-kernels, general-purpose sandboxing, danger, Kernel namespaces, seccomp, Linux kernel capabilities.

### Access control model of web ecosystem, single-origin policy, preservations of integrity of data and code, sandboxing in web, content security policy.

### Network protocols, TCP, DNS, BGP, security of HTTPs, mechanism of certificates, security of certificate infrastructure.

### Firewalls, network intrusion detection, network intrusion prevention, thin client, intrusion deflection.

### Denial of service attack, reflection attacks, syn-cookies, detection and protection against DOS.