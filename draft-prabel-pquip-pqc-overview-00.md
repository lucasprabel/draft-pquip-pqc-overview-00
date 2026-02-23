---

###
title: "Post-Quantum Algorithms Overview"
abbrev: "PQC Algo Overview"
category: info

docname: draft-prabel-pquip-pqc-overview-00
submissiontype: IETF  # also: "independent", "editorial", "IAB", or "IRTF"
number:
date:
consensus: true
v: 0
area: Security
workgroup: PQUIP
keyword:
 - PQUIP
 - Migration
 - PQC
 - Parameters
 - Algorithms
venue:
  group: Post-Quantum Use In Protocols
  type: Working Group
  mail: pqc@ietf.org
  arch: https://mailarchive.ietf.org/arch/browse/pqc/
  github: lucasprabel/draft-pquip-pqc-overview-00

author:
 -  ins: L. Prabel
    fullname: Lucas Prabel
    organization: Huawei
    email: lucas.prabel@huawei.com
 -  ins: Y. Shah
    fullname: Yug Shah
    organization: Qorsa
    email: yug.shah@qorsa.com
 -  ins: G. Wang
    fullname: Guilin Wang
    organization: Huawei
    email: wang.guilin@huawei.com
 -  ins: S. Kanno
    fullname: Satoru Kanno
    organization: GMO Internet Group
    email: kanno@gmo-connect.jp

informative:
 RFC8554:
 I-D.draft-ietf-pquip-hbs-state: HBS-STATE
 MLKEM.SPEC:
    title: "Module-Lattice-Based Key-Encapsulation Mechanism Standard"
    date: August 2024
    author:
      org: "National Institute of Standards and Technology (NIST)"
    target: https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.203.pdf
 FRODOKEM.SPEC:
    title: "FrodoKEM: Learning With Errors Key Encapsulation"
    date: December 2024
    author:
      org:
    target: https://frodokem.org/files/FrodoKEM_standard_proposal_20241205.pdf
 CLASSICMCELIECE.SPEC:
    title: "Classic McEliece: conservative code-based cryptography"
    date: October 2022
    author:
      org:
    target: https://classic.mceliece.org/mceliece-spec-20221023.pdf
 HQC.SPEC:
    title: "Hamming Quasi-Cyclic (HQC)"
    date: February 2025
    author:
      org:
    target: https://pqc-hqc.org/doc/hqc-specification_2025-02-19.pdf
 NTRU.SPEC:
    title: "NTRU Key Encapsulation"
    date: March 2025
    author:
      org:
    target: https://www.ietf.org/id/draft-fluhrer-cfrg-ntru-02.html
 MLDSA.SPEC:
    title: "Module-Lattice-Based Digital Signature Standard"
    date: August 2024
    author:
      org:
    target: https://nvlpubs.nist.gov/nistpubs/fips/nist.fips.204.pdf
 FNDSA.SPEC:
    title: "Falcon: Fast-Fourier Lattice-based Compact Signatures over NTRU"
    date: October 2020
    author:
      org:
    target: https://falcon-sign.info/falcon.pdf
 SLHDSA.SPEC:
    title: "Stateless Hash-Based Digital Signature Standard"
    date: August 2024
    author:
      org:
    target: https://nvlpubs.nist.gov/nistpubs/FIPS/NIST.FIPS.205.pdf
 LMS.SPEC:
    title: "Recommendation for Stateful Hash-Based Signature Schemes"
    date: October 2020
    author:
      org:
    target: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-208.pdf
 XMSS.SPEC:
    title: "Recommendation for Stateful Hash-Based Signature Schemes"
    date: October 2020
    author:
      org:
    target: https://nvlpubs.nist.gov/nistpubs/SpecialPublications/NIST.SP.800-208.pdf
 IR.8547:
    title: "Transition to Post-Quantum Cryptography Standards"
    date: November 2024
    author:
      org: "National Institute of Standards and Technology (NIST)"
    target: https://nvlpubs.nist.gov/nistpubs/ir/2024/NIST.IR.8547.ipd.pdf
 EU.Roadmap:
    title: "A Coordinated Implementation Roadmap for the Transition to Post-Quantum Cryptography"
    date: June 2025
    author:
      org: "EU PQC Workstream"
    target: https://digital-strategy.ec.europa.eu/en/library/coordinated-implementation-roadmap-transition-post-quantum-cryptography
 TNO.Handbook:
    title: "The PQC Migration Handbook"
    date: December 2024
    author:
      org: "AIVD, CWI, TNO"
    target: https://publications.tno.nl/publication/34643386/fXcPVHsX/TNO-2024-pqc-en.pdf
 ANSSI.PQCMigration:
    title: "Avis de l'ANSSI sur la migration vers la cryptographie post-quantique (suivi 2023)"
    date: December 2023
    author:
      org: "ANSSI"
    target: https://messervices.cyber.gouv.fr/documents-guides/Avis%20de%20l%27ANSSI%20sur%20la%20migration%20vers%20la%20cryptographie.pdf
 ANSSI.PQCViews:
    title: "Cryptographic Mechanisms: Recommendations and Key Lengths"
    date: March 2025
    author:
      org: "ANSSI"
    target: https://na.eventscloud.com/file_uploads/b635298de1c10be6d3732863e8b1beca_Day2-1600-ANSSI.pdf
 BSI.PQCMigration:
    title: "Cryptographic Mechanisms: Recommendations and Key Lengths"
    date: January 2025
    author:
      org: "ANSSI"
    target: https://www.bsi.bund.de/SharedDocs/Downloads/EN/BSI/Publications/TechGuidelines/TG02102/BSI-TR-02102-1.pdf?__blob=publicationFile&v=10



--- abstract

This document summarizes publicly available information on a range of widely studied post-quantum cryptographic algorithms, including Key Encapsulation Mechanisms (KEMs) and digital signature schemes.

It aggregates parameters and high-level security assumptions from existing specifications and standardization efforts, serving as a unified informational reference.

This document is purely informational. It does not provide guidance, recommendations, or requirements regarding algorithm selection, deployment, or migration strategies.

--- middle

# Introduction

The emergence of large-scale quantum computers poses a significant threat to widely deployed asymmetric cryptographic algorithms that rely on integer factorization or discrete logarithms. In response, the cryptographic community has developed post-quantum cryptographic (PQC) algorithms designed to resist attacks from both classical and quantum adversaries.

Several standardization bodies, including NIST, ISO, and others, have been evaluating and standardizing post-quantum algorithms for key encapsulation mechanisms (KEMs) and digital signature schemes. As these algorithms advance through various standardization processes, implementers and protocol designers need readily accessible reference information about their parameters, security properties, and characteristics.

This document provides a consolidated overview of widely studied post-quantum cryptographic algorithms, based on publicly available information. It aggregates parameter sizes, security classifications, and underlying hardness assumptions from existing specifications and standardization efforts. The information presented here is purely informational and does not constitute recommendations or requirements for algorithm selection, deployment strategies, or migration planning.

The document covers both KEM schemes (ML-KEM, HQC, FrodoKEM, NTRU, Classic McEliece) and signature schemes (ML-DSA, FN-DSA, SLH-DSA, LMS, XMSS/XMSS^MT), providing a unified reference to assist stakeholders in navigating the landscape of post-quantum cryptographic algorithms.


# Conventions and Definitions

{::boilerplate bcp14-tagged}

This section recalls terminology relevant to post-quantum cryptographic algorithms and defines additional terms used throughout this document.

*CRQC*: A Cryptographically Relevant Quantum Computer is a quantum 
   computer powerful enough to break traditional asymmetric 
   cryptographic algorithms.


*Traditional Asymmetric Cryptographic Algorithm*:  An asymmetric
   cryptographic algorithm based on integer factorisation, finite
   field discrete logarithms, elliptic curve discrete logarithms, or
   related mathematical problems. They can also be called classical or
   conventional algorithms.

*Post-Quantum Asymmetric Cryptographic Algorithm*:  An asymmetric 
cryptographic algorithm whose security is intended to hold against 
attacks using either classical or quantum computational resources.
They can also be called quantum-resistant or quantum-safe algorithms.

As with all cryptography, it always remains the case that attacks, either quantum or classical, may be found against post-quantum algorithms. Therefore it should not be assumed that just because an algorithm is designed to provide post-quantum security it will not be compromised. Post-Quantum Algorithms are named for their design objective: security against an adversary with access to a CRQC, and this classification will remain should an attack be found against it.

*IND-CCA2*: Indistinguishability under Adaptive Chosen-Ciphertext Attack. It is the standard security notion for KEM schemes.

*EUF-CMA*: Existential Unforgeability under Chosen-Message Attack. It is the standard security notion for digital signature schemes.

*SUF-CMA*: Strong Existential Unforgeability under Chosen-Message Attack. It is a stronger security notion than EUF-CMA.

# Parameter Sizes

This section is divided into two subsections, one focused on Key Encapsulation Mechanism, and the other on Signature schemes.

The "claimed security level" in each table refers to the NIST Post-Quantum Cryptography Evaluation Criteria. We summarize this classification in {{tab-security-level}} below. Additional details are available at {{ IR.8547 }}.

| Security Category | Attack Type | Example |
| ----------- | ----------- | ----------- |
| 1 | Key search on a block cipher with a 128-bit key  | AES-128 |
| 2 | Collision search on a 256-bit hash function  | SHA-256 |
| 3 | Key search on a block cipher with a 192-bit key | AES-192 |
| 4 | Collision search on a 384-bit hash function | SHA3-384
| 5 | Key search on a block cipher with a 256-bit key | AES-256 |
{: #tab-security-level title="NIST Post-Quantum Cryptography Classification"}

## Key Encapsulation Mechanism (KEM) Schemes

A Key Encapsulation Mechanism (KEM) is a cryptographic primitive that can be used as a building block within a broader key establishment protocol. While KEMs are often employed to achieve the same end goal as a traditional key exchange, they do not, by themselves, define the interactive procedures, message flows, or authentication steps that a full key exchange protocol requires.

This distinction is particularly relevant for implementers and developers to avoid confusion:

- A KEM provides the mechanism for securely deriving and encapsulating a shared secret.
- A Key Exchange Protocol defines the interaction between parties that uses one or more KEMs (and possibly other primitives) to securely establish a secret key in context.

### ML-KEM

ML-KEM is a structured lattice-based KEM and the first post-quantum KEM standardized by NIST. It is derived from the CRYSTALS-Kyber submission to NIST PQC Standardization Project. The security of ML-KEM is based on the computational hardness of the Module Learning with Errors problem.

NIST recommends security level 3 by default, and European security agencies recommend a minimum of the same security level.

The NIST specification of ML-KEM is available at {{MLKEM.SPEC}}.


| Scheme | Public Key | Private Key | Ciphertext | Shared Secret | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- | ----------- |
| ML-KEM-512 | 800 | 1632 | 768 | 32 | 1 |
| ML-KEM-768 | 1184 | 2400 | 1088 | 32 | 3 |
| ML-KEM-1024 | 1568 | 3168 | 1568 | 32 | 5 |
{: #tab-mlkem title="ML-KEM Parameter Sizes (in bytes)"}

{{MLKEM.SPEC}} also allows the use of a 64-byte seed to represent the private key.


### HQC

HQC is a code-based KEM relying on the decisional Quasi-Cyclic Syndrome Decoding (QCSD) hardness assumption.

It has been selected for standardization by NIST.

The HQC specification is available at {{HQC.SPEC}}.


| Scheme | Public Key | Private Key | Ciphertext | Shared Secret | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- | ----------- |
| HQC-128 | 2249 | 2305 | 4433 | 64 | 1 |
| HQC-192 | 4522 | 4586 | 8978 | 64 | 3 |
| HQC-256 | 7245 | 7317 | 14421 | 64 | 5 |
{: #tab-hqc title="HQC Parameter Sizes (in bytes)"}


### FrodoKEM

FrodoKEM is a lattice-based KEM whose security is based on the Learning with Errors (LWE) hardness assumption. Unlike the structured lattices of ML-KEM, FrodoKEM uses unstructured lattices.

FrodoKEM is being standardized by ISO, and it is mentioned in guidance published by several European security agencies ({{ TNO.Handbook }}, {{ ANSSI.PQCMigration }}, {{ BSI.PQCMigration }}). Some of these agencies recommend in particular the security levels 3 and 5.

The FrodoKEM specification is available at {{FRODOKEM.SPEC}}. It includes variants using AES or SHAKE as underlying primitives. Implementations may differ in performance characteristics depending on available hardware support.


| Scheme | Public Key | Private Key | Ciphertext | Shared Secret | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- | ----------- |
| FrodoKEM-640-AES  | 9616 | 19888 | 9720 | 16 | 1 |
| FrodoKEM-640-SHAKE  | 9616 | 19888 | 9720 | 16 | 1 |
| FrodoKEM-976-AES  | 15632 | 31296 | 15744 | 24 | 3 |
| FrodoKEM-976-SHAKE  | 15632 | 31296 | 15744 | 24 | 3 |
| FrodoKEM-1344-AES  | 21520 | 43088 | 21632 | 32 | 5 |
| FrodoKEM-1344-SHAKE  | 21520 | 43088 | 21632 | 32 | 5 |
{: #tab-frodokem title="FrodoKEM Parameter Sizes (in bytes)"}


### NTRU

NTRU is a structured lattice-based KEM.

It is being standardized by ISO.

The NTRU specification is available at {{NTRU.SPEC}}.

| Scheme | Public Key | Private Key | Ciphertext | Shared Secret | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- | ----------- |
| ntruhps2048509 | 699 | 935 | 699 | 32 | 1 |
| ntruhps2048677 | 930 | 1235 | 930 | 32 | 3 |
| ntruhps4096821 | 1230 | 1592 | 1230 | 32 | 5 |
| ntruhrss701 | 1138 | 1452 | 1138 | 32 | 3 |
| ntruhrss1373 | 2401 | 2983 | 2401 | 32 | 5 |
{: #tab-ntru title="NTRU Parameter Sizes (in bytes)"}


### Classic McEliece

Classic McEliece is a code-based KEM, based on the original McEliece cryptosystem from 1978.

It is being standardized by ISO. Some European security agencies recommend it with specific parameter sets ({{ TNO.Handbook }}, {{ BSI.PQCMigration }}) while ANSSI doesn't recommend it anymore ({{ ANSSI.PQCViews }}).

Each security level includes a 'f' variant that enables faster key generation, but is internally more complex.

The Classic McEliece specification is available at {{CLASSICMCELIECE.SPEC}}.


| Scheme | Public Key | Private Key | Ciphertext | Shared Secret | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- | ----------- |
| Classic-McEliece-348864  | 261120 | 6492 | 96 | 32 | 1 |
| Classic-McEliece-348864f  | 261120 | 6492 | 96 | 32 | 1 |
| Classic-McEliece-460896  | 524160	| 13608 | 156 | 32 | 3 |
| Classic-McEliece-460896f  | 524160 | 13608 | 156 | 32 | 3 |
| Classic-McEliece-6688128  | 1044992 | 13932 | 208 | 32 | 5 |
| Classic-McEliece-6688128f  | 1044992 | 13932 | 208 | 32 | 5 |
| Classic-McEliece-6960119  | 1047319 | 13948 | 194 | 32 | 5 |
| Classic-McEliece-6960119f  | 1047319 | 13948 | 194 | 32 | 5 |
| Classic-McEliece-8192128  | 1357824 | 14120 | 208 | 32 | 5 |
| Classic-McEliece-8192128f  | 1357824 | 14120 | 208 | 32 | 5 |
{: #tab-cme title="Classic-McEliece Parameter Sizes (in bytes)"}


## Signature Schemes

Digital signatures are cryptographic primitives used to provide authenticity, integrity, and non-repudiation of messages or data. 

In the context of post-quantum cryptography, signature schemes are designed to remain secure against adversaries with quantum computing capabilities. They can be used in various scenarios, including authentication of protocol messages, code signing, and certificates, and are often combined with key establishment mechanisms in secure communication protocols.


### ML-DSA

ML-DSA is a structured lattice-based signature scheme, now standardized by NIST. It is derived from the CRYSTALS-Dilithium submission to NIST PQC Standardization Project. The security of ML-DSA is based on the computational hardness of the Module Learning with Errors problem as well as the SelfTargetMSIS problem, a variant of the Module Short Integer Solution problem.

European security agencies recommend at least security level 3.

The NIST specification of ML-DSA is available at {{MLDSA.SPEC}}.


| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| ML-DSA-44  | 1312 | 2560 | 2420 | 2 |
| ML-DSA-65  | 1952 | 4032 | 3309 | 3 |
| ML-DSA-87  | 2592 | 4896 | 4627 | 5 |
{: #tab-mldsa title="ML-DSA Parameter Sizes (in bytes)"}

{{MLDSA.SPEC}} also allows to use a 32-bytes seed to represent the private key.


### FN-DSA

FN-DSA, formerly known as Falcon, is a lattice-based signature scheme that was selected by NIST for standardization.

FN-DSA relies on floating-point arithmetic as part of its design, and the specification is available at {{FNDSA.SPEC}}.

FN-DSA signatures can be generated in two formats: compressed (Falcon-512 and Falcon-1024) and padded (Falcon-padded-512 and Falcon-padded-1024). The compressed version results in variable-length signatures, shorter on average, while the padded version ensures a constant signature size. In {{tab-fndsa}}, the indicated variable-length signature size is a maximum.


| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| Falcon-512  | 897 | 1281 | 752 | 1 |
| Falcon-1024  | 1793 | 2305 | 1462 | 5 |
| Falcon-padded-512  | 897 | 1281 | 666 | 1 |
| Falcon-padded-1024  | 1793 | 2305 | 1280 | 5 |
{: #tab-fndsa title="FN-DSA Parameter Sizes (in bytes)"}


### SLH-DSA

SLH-DSA is a stateless hash-based signature scheme standardized by NIST. It is derived from the SPHINCS+ submission to NIST PQC Standardization Project.

Each security level offers two possible hash function families (SHA-2 or SHAKE), and for each family, two specific variants: the 's' (small signature) variant and the 'f' (fast generation) variant. Each parameter set defines choices affecting signature size and performance characteristics.

The NIST specification of SLH-DSA is available at {{SLHDSA.SPEC}}.

| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| SLH-DSA-SHA2-128s | 32 | 64 | 7856 | 1 |
| SLH-DSA-SHAKE-128s | 32 | 64 | 7856 | 1 |
| SLH-DSA-SHA2-128f | 32 | 64 | 17088 | 1 |
| SLH-DSA-SHAKE-128f | 32 | 64 | 17088 | 1 |
| SLH-DSA-SHA2-192s | 48 | 96 | 16224 | 3 |
| SLH-DSA-SHAKE-192s | 48 | 96 | 16224 | 3 |
| SLH-DSA-SHA2-192f | 48 | 96 | 35664 | 3 |
| SLH-DSA-SHAKE-192f | 48 | 96 | 35664 | 3 |
| SLH-DSA-SHA2-256s | 64 | 128 | 29762 | 5 |
| SLH-DSA-SHAKE-256s | 64 | 128| 29762 | 5 |
| SLH-DSA-SHA2-256f | 64 | 128 | 49856 | 5 |
| SLH-DSA-SHAKE-256f | 64 | 128 | 49856 | 5 |
{: #tab-slhdsa title="SLH-DSA Parameter Sizes (in bytes)"}

### LMS

Leighton-Micali Signatures (LMS) is a stateful hash-based signature scheme based on Merkle hash trees that uses Leighton-Micali One-Time Signatures (LM-OTS) as its component one-time signature scheme. When referring to specific parameter sets and algorithm identifiers in the following tables, the hyphen is omitted (LMOTS) in accordance with the nomenclature established in NIST SP 800-208 {{LMS.SPEC}} and RFC 8554 {{RFC8554}} .

It requires careful state management. {{-HBS-STATE}} provides guidance and security considerations on state management for stateful hash-based signature schemes.

The NIST specification of LMS is available at {{LMS.SPEC}}.

#### LMS with SHA-256

The signatures' sizes for the LMS_SHA256_M32_H{5, 10, 15, 20, 25} signature scheme depend on the choice of the underlying LMOTS scheme and in particular on the value of the Winternitz parameter W. Therefore, the signatures' sizes of LMS_SHA256_M32_H{5, 10, 15, 20, 25} are given in a 4-element array where values correspond to the value of W = 8, 4, 2, 1 in that order.

| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| LMOTS_SHA256_N32_W1  | 56 | 8504 | 8516 | x | 
| LMOTS_SHA256_N32_W2  | 56 | 4280 | 4292 | x |
| LMOTS_SHA256_N32_W4  | 56 | 2168 | 2180 | x |
| LMOTS_SHA256_N32_W8  | 56 | 1112 | 1124 | x |
| LMS_SHA256_M32_H5 | 56 | 1796 | [1296, 2352, 4464, 8688] | 5 |
| LMS_SHA256_M32_H10 | 56 | 57348 | [1456, 2512, 4624, 8848] | 5 |
| LMS_SHA256_M32_H15 | 56 | 1835012 | [1616, 2672, 4784, 9008] | 5 |
| LMS_SHA256_M32_H20 | 56 | 58720260 | [1776, 2832, 4944, 9168] | 5 |
| LMS_SHA256_M32_H25 | 56 | 1879048196 | [1936, 2992, 5104, 9328] | 5 |
{: #tab-lms-sha256 title="LMS with SHA256 Parameter Sizes (in bytes)"}

#### LMS with SHA-256/192

The signatures' sizes for the LMS_SHA256/192_M24_H{5, 10, 15, 20, 25} signature scheme depend on the choice of the underlying LMOTS scheme and in particular on the value of the Winternitz parameter W. Therefore, the signatures' sizes of LMS_SHA256/192_M24_H{5, 10, 15, 20, 25} are given in a 4-element array where values correspond to the value of W = 8, 4, 2, 1 in that order.

| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| LMOTS_SHA256_N24_W1  | 56 | 4824 | 4828 | x |
| LMOTS_SHA256_N24_W2  | 56 | 2448 | 2452 | x |
| LMOTS_SHA256_N24_W4  | 56 | 1248 | 1251 | x |
| LMOTS_SHA256_N24_W8  | 56 | 648 | 652 | x |
| LMS_SHA256_M24_H5  | 56 | 1796 | [784, 1384, 2584, 4960] | 3 |
| LMS_SHA256_M24_H10 | 56 | 57348 | [904, 1504, 2704, 5080] | 3 |
| LMS_SHA256_M24_H15 | 56 | 1835012 | [1024, 1624, 2824, 5200] | 3 |
| LMS_SHA256_M24_H20 | 56 | 58720260 | [1144, 1744, 2944, 5320] | 3 |
| LMS_SHA256_M24_H25 | 56 | 1879048196 | [1264, 1864, 3064, 5440] | 3 |
{: #tab-lms-sha256/192 title="LMS with SHA256/192 Parameter Sizes (in bytes)"}

#### LMS with SHAKE256/256

The signatures' sizes for the LMS_SHAKE_M32_H{5, 10, 15, 20, 25} signature scheme depend on the choice of the underlying LMOTS scheme and in particular on the value of the Winternitz parameter W. Therefore, the signatures' sizes of LMS_SHA256_M32_H{5, 10, 15, 20, 25} are given in a 4-element array where values correspond to the value of W = 8, 4, 2, 1 in that order.

| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| LMOTS_SHAKE_N32_W1  | 56 | 8504 | 8516 | x |
| LMOTS_SHAKE_N32_W2  | 56 | 4280 | 4292 | x |
| LMOTS_SHAKE_N32_W4  | 56 | 2168 | 2180 | x |
| LMOTS_SHAKE_N32_W8  | 56 | 1112 | 1124 | x |
| LMS_SHAKE_M32_H5  | 56 | 1796 | [1296, 2352, 4464, 8688] | 5 |
| LMS_SHAKE_M32_H10 | 56 | 57348 | [1456, 2512, 4624, 8848] | 5 |
| LMS_SHAKE_M32_H15 | 56 | 1835012 | [1616, 2672, 4784, 9008] | 5 |
| LMS_SHAKE_M32_H20 | 56 | 58720260 | [1776, 2832, 4944, 9168] | 5 |
| LMS_SHAKE_M32_H25 | 56 | 1879048196 | [1936, 2992, 5104, 9328] | 5 |
{: #tab-lms-shake256/256 title="LMS with SHAKE256/256 Parameter Sizes (in bytes)"}

#### LMS with SHAKE256/192

The signatures' sizes for the LMS_SHAKE_M24_H{5, 10, 15, 20, 25} signature scheme depend on the choice of the underlying LMOTS scheme and in particular on the value of the Winternitz parameter W. Therefore, the signatures' sizes of LMS_SHA256/192_M24_H{5, 10, 15, 20, 25} are given in a 4-element array where values correspond to the value of W = 8, 4, 2, 1 in that order.

| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| LMOTS_SHAKE_N24_W1  | 56 | 4824 | 4828 | x |
| LMOTS_SHAKE_N24_W2  | 56 | 2448 | 2452 | x |
| LMOTS_SHAKE_N24_W4  | 56 | 1248 | 1252 | x |
| LMOTS_SHAKE_N24_W8  | 56 | 648 | 652 | x |
| LMS_SHAKE_M24_H5  | 56 | 1796 | [784, 1384, 2584, 4960] | 3 |
| LMS_SHAKE_M24_H10 | 56 | 57348 | [904, 1504, 2704, 5080] | 3 |
| LMS_SHAKE_M24_H15 | 56 | 1835012 | [1024, 1624, 2824, 5200] | 3 |
| LMS_SHAKE_M24_H20 | 56 | 58720260 | [1144, 1744, 2944, 5320] | 3 |
| LMS_SHAKE_M24_H25 | 56 | 1879048196 | [1264, 1864, 3064, 5440] | 3 |
{: #tab-lms-shake256/192 title="LMS with SHAKE256/192 Parameter Sizes (in bytes)"}


### XMSS / XMSS^MT

The eXtended Merkle Signature Scheme (XMSS) is a stateful hash-based signature scheme that uses WOTS+ for one-time signatures, and is based on Merkle hash trees. XMSS^MT is a variant that has multiple hash trees.

It requires careful state management. {{-HBS-STATE}} provides guidance and security considerations on state management for stateful hash-based signature schemes.

The NIST specification of XMSS is available at {{XMSS.SPEC}}.

| Scheme | Public Key | Private Key | Signature | Claimed security level |
| ----------- | ----------- |  ----------- | ----------- | ----------- |
| XMSS-SHA2_10_256| 64 | 1373 | 2500 | 5 |
| XMSS-SHA2_16_256 | 64 | 2093 | 2692 | 5 |
| XMSS-SHA2_20_256 | 64 | 2573 | 2820 | 5 |
| XMSSMT-SHA2_20/2_256 | 64 | 5998 | 4963 | 5 |
| XMSSMT-SHA2_20/4_256 | 64 | 10938 | 9251 | 5 |
| XMSSMT-SHA2_40/2_256 | 64 | 9600 | 5605 | 5 |
| XMSSMT-SHA2_40/4_256 | 64 | 15252 | 9893 | 5 |
| XMSSMT-SHA2_40/8_256 | 64 | 24516 | 18469 | 5 |
| XMSSMT-SHA2_60/3_256 | 64 | 16629 | 8392 | 5 |
| XMSSMT-SHA2_60/6_256 | 64 | 24507 | 14824 | 5 |
| XMSSMT-SHA2_60/12_256 | 64 | 38095 | 27688 | 5 |
| XMSS-SHA2_10_192| 48 | 1053 | 1492 | 3 |
| XMSS-SHA2_16_192 | 48 | 1605 | 1636 | 3 |
| XMSS-SHA2_20_192 | 48 | 1973 | 1732 | 3 |
| XMSS-SHAKE256_10_256| 64 | 1373 | 2500 | 5 |
| XMSS-SHAKE256_16_256 | 64 | 2093 | 2692 | 5 |
| XMSS-SHAKE256_20_256 | 64 | 2573 | 2820 | 5 |
| XMSSMT-SHAKE256_20/2_256| 64 | 5998 | 4963 | 5 |
| XMSSMT-SHAKE256_20/4_256 | 64 | 10938 | 9251 | 5 |
| XMSSMT-SHAKE256_40/2_256 | 64 | 9600 | 5605 | 5 |
| XMSSMT-SHAKE256_40/4_256 | 64 | 15252 | 9893 | 5 |
| XMSSMT-SHAKE256_40/8_256 | 64 | 24516 | 18469 | 5 |
| XMSSMT-SHAKE256_60/3_256 | 64 | 16629 | 8392 | 5 |
| XMSSMT-SHAKE256_60/6_256 | 64 | 24507 | 14824 | 5 |
| XMSSMT-SHAKE256_60/12_256 | 64 | 38095 | 27688 | 5 |
| XMSS-SHAKE256_10_192| 48 | 1053 | 1492 | 3 |
| XMSS-SHAKE256_16_192 | 48 | 1605 | 1636 | 3 |
| XMSS-SHAKE256_20_192 | 48 | 1973 | 1732 | 3 |
{: #tab-xmss title="XMSS Parameter Sizes (in bytes)"}


# Security Considerations

## Quantum-Vulnerable Asymmetric Cryptography

{{tab-vulne}} gives a list of asymmetric cryptographic schemes that are vulnerable to quantum computers and are planned to be deprecated and/or disallowed in the future by various organizations or security agencies. In particular, NIST provides deprecation and disallowance timelines in {{ IR.8547 }}.

The EU PQC Workstream also published its roadmap for the transition to post-quantum cryptography in {{ EU.Roadmap }}. It distinguishes between low, medium and high quantum risk levels, and recommends completing the PQC transition for high-risk use cases before 2031, for medium-risk use cases before 2036, and for low-risk use cases before 2036, as much as feasible.



| Scheme | Hardness assumption | Disallowed (NIST) |
| ----------- | ----------- | ----------- |
| ECDSA | Elliptic Curve Discrete Logarithm | after 2035 |
| EdDSA | Elliptic Curve Discrete Logarithm | after 2035 |
| RSA | Factorisation | after 2035 |
| (EC)DH | (Elliptic Curve) Computational/Decisional DH | after 2035 |
{: #tab-vulne title=" Quantum-Vulnerable Asymmetric Cryptographic Schemes"}

## Quantum-Safe Asymmetric Cryptography

{{tab-secu-kem}} gives a brief summary of the security properties of various KEM algorithms.

| Scheme | SDO | Hardness assumption | Security Model | Comments |
| ----------- | ----------- | ----------- | ----------- |----------- |
| ML-KEM | NIST | Module LWE | IND-CCA2 | |
| FrodoKEM | ISO | Unstructured LWE | IND-CCA2 | |
| HQC | NIST | Decisional Quasi-Cyclic Syndrome Decoding Problem | IND-CCA2  | |
| Classic McEliece | ISO | Syndrome Decoding Problem, Goppa code recovery|IND-CCA2 | |
| NTRU | ISO | NTRU | IND-CCA2  | |
{: #tab-secu-kem title="Properties of KEM schemes"}

{{tab-secu-sig}} gives a summary of the security properties of different signature algorithms.

| Scheme | SDO | Hardness assumption | Security Model | Comments |
| ----------- | ----------- | ----------- | ----------- |----------- |
| ML-DSA | NIST | Module LWE, SelfTargetMSIS | SUF-CMA | |
| FN-DSA | NIST | SIS over NTRU lattices | EUF-CMA | Uses floating point arithmetic |
| SLH-DSA | NIST | Second-preimage resistance | SUF-CMA (*) | |
| LMS | NIST | Collision resistance | SUF-CMA (*) | Need state management |
| XMSS | NIST | Collision resistance | SUF-CMA (*) | Need state management |
{: #tab-secu-sig title=" Properties of signatures schemes"}
(*) There is no known attack on the SUF-CMA security of those schemes, which are widely believed to be SUF-CMA secure. However, no formal proof exists yet.

## Evolving Cryptanalysis

Security analysis of post-quantum cryptographic schemes is an area of active research. The security levels indicated in this document reflect current claims based on existing knowledge. However, these may evolve as cryptanalysis improves.

## Caveats for Implementers

The transition to post-quantum algorithms introduces several technical aspects that differ from traditional asymmetric cryptography:

- Side-Channel Analysis: some of the post-quantum schemes presented in this document could present new surfaces for side-channel attacks and the relative complexity of their design could make constant-time implementations more challenging.
- State Management: stateful hash-based signatures (LMS and XMSS) require the signer to maintain a persistent and accurate record of used one-time keys. Failure to properly manage this state can lead to a catastrophic loss of security for the private key. See {{-HBS-STATE}} for more details.
- Resource Constraints: the increased size of public keys, private keys, and signatures/ciphertexts may impact protocols with maximum transmission unit (MTU) limitations or devices with restricted memory and bandwidth.


# IANA Considerations

This document has no IANA action.

# Acknowledgments

We thank Sun Shuzhou and Zeng Guang for their valuable comments and recommendations on this document.
