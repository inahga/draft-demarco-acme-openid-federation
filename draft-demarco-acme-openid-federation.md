---
title: "Automatic Certificate Management Environment (ACME) with OpenID Connect Federation 1.0"
abbrev: "ACME OIDC Federation"
category: std

docname: draft-demarco-acme-openid-federation-latest
submissiontype: IETF  # also: "independent", "IAB", or "IRTF"
number:
date:
consensus: true
v: 3
area: "Security"
workgroup: "Automated Certificate Management Environment"
keyword:
 - OpenID Connect Federation
 - ACME
venue:
  group: "Automated Certificate Management Environment"
  type: "Working Group"
  mail: "acme@ietf.org"
  arch: "https://mailarchive.ietf.org/arch/browse/acme/"
  github: "peppelinux/draft-demarco-acme-openid-federation"

author:
 -
    fullname: Giuseppe De Marco
    organization: independent
    email: demarcog83@gmail.com

normative:
  RFC2818: RFC2818
  RFC3696: RFC3696
  RFC8555: RFC8555

  OIDC-FED:
    title: "OpenID Connect Federation 1.0"
    author:
      -
        ins: R. Hedberg
        name: Roland Hedberg
      -
        ins: M.B. Jones
        name: Michael Jones
      -
        ins: A.Å. Solberg
        name: Andreas Solberg
      -
        ins: J. Bradley
        name: John Bradley
      -
        ins: G. De Marco
        name: Giuseppe De Marco
      -
        ins: V. Dzhuvinov
        name: Vladimir Dzhuvinov

informative:


--- abstract

This document defines how the X.509 certificates can be issued by a trust anchor and its intermediates through the ACME protocol to all the organizations that are part of a federation built on top of OpenID Connect Federation 1.0.

--- middle

# Introduction

The Automatic Certificate Management Environment (ACME) is the standard [RFC8555] that allows obtaining certificates for websites (HTTPS [RFC2818]) by verifing the "fully-qualified" domain names [RFC3696] and the web servers within these.

OpenID Connect Federation 1.0 [OIDC-FED] is the standard that allows building multilateral federations through a trust evaluation mechanism attesting the possession of public keys, signature capabilities, protocol specific metadata and several administrative and tecnical information in the form of trust marks, related to a specific entity belonging to an organization.

OpenID Connect Federation 1.0 allows an ACME server to issue X.509 certificates to one or more than a single organization without having pre-established any direct relationship or any stipulation of a contract to the requestor. In a multilateral federation, composed by thousands of entities belonging to different organizations, all the participants adhere to the same regulation or trust framework. OpenID Connect Federation 1.0 allows each participant to recognize the other participant using a trust evaluation mechanism, using RESTful services and cryptographic materials.

Considering that a requestor is an entity requesting the issuance of a X.509 certificate to a server and the issuer is the ACME server that validates the entitlements of the requestor before issuing the X.509 certificate, this specification defines how ACME and OpenID Connect Federation 1.0 can be integrated allowing an efficient issuance of X.509 to a requestor, reducing both the bureaucratic and the implementative costs, since:

- It does not require the involvement of other resources than the ACME `newOrder` endpoint, since the authentication and authorization of the requestor is asserted with OpenID Federation 1.0.
- Instead of the `/.well-known/acme-challenge/{token}` endpoint it defines how to use and validate a basic OpenID Connect Federation component, called Entity Configuration, that is a signed JWT published in a well-known resource (.well-known/openid-federation) published by the requestor.
- It removes the requirement for the authentication of an entity and the provisioning of the *acme-challenge token*, since the authorization mechanisms is built on top of the trust evaluation model as defined in OpenID Connect Federation 1.0.
- It extends the ACME `newOrder` endpoint, defining a new payload identifier type called `openid-federation`.
- It defines how the OpenID Federation Entity Statements can be used for the publication of the X.509 certificates, by a trust anchor or intermediate, that was previously issued with ACME.

# Conventions and Definitions

{::boilerplate bcp14-tagged}

# Audience Target audience/Usage

The audience of the document are the multilateral federations that require automatic issuance oif X.509 certificates using an infrastructure of trust based on OpenID Connect Federation 1.0.

# Scope

This specification defines how a [OIDC-FED] Federation API is used by ACME in the authorization phase for the issuance of the certificates.

# Security Considerations

TODO Security


# IANA Considerations

This document has no IANA actions.


--- back

# Acknowledgments
{:numbered="false"}

TODO acknowledge.