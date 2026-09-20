# Tinytums: Understanding ABDM & ABHA

## Plain-language orientation \+ developer starting guide

Purpose: Help the Tinytums clinical, product and developer teams understand how ABDM works before designing the detailed integration and compliance matrix.

Important note:  
This is an orientation document, not a substitute for the current ABDM Sandbox specification, security requirements or legal advice. ABDM specifications evolve. When implementation begins, the team should always use the then-current official NHA/ABDM Sandbox documentation and the currently published ABDM FHIR Implementation Guide.

# PART A — THE “WHAT”: ABDM IN SIMPLE LANGUAGE

## 1\. The one-minute explanation

**Ayushman Bharat Digital Mission (ABDM)** is India’s national digital-health ecosystem. It is designed so that patients, doctors, hospitals, laboratories and health applications can identify one another and exchange health information in a standardized, consent-based and secure way.  
The most important idea is this: ABDM is not simply one giant government medical-record database. Its architecture is federated. In simple terms, the record normally remains with the hospital, clinic, laboratory or digital system that created/holds it, while ABDM provides the identity, discovery, consent and exchange framework that allows authorized systems to communicate.

Think of ABDM like a trusted health-information network:

Patient identity      Doctor identity      Facility identity

     |                     |                     |

    ABHA                  HPR                   HFR

     \\                     |                    /

      \\                    |                   /

       \+---------- ABDM trust layer \----------+

                    |

                    \+-- consent

                    \+-- record discovery/linking

                    \+-- secure exchange

                    \+-- interoperability standards

                    |

              Hospital / Lab / App

              keeps the actual record

## 2\. Who sits where?

Government of India

        |

        v

Ministry of Health & Family Welfare (MoHFW)

        |

        v

National Health Authority (NHA)

        |

        v

Ayushman Bharat Digital Mission (ABDM)

        |

        \+-- ABHA  : patient identity / health account

        \+-- HPR   : healthcare professional registry

        \+-- HFR   : health facility registry

        \+-- PHR   : patient-controlled health-record functions

        \+-- HIE / consent infrastructure

        \+-- FHIR-based health-data exchange standards

For Tinytums, the practical authority to watch is NHA/ABDM because that is where the integration ecosystem, sandbox and implementation requirements come from.

## 3\. Essential abbreviations and what they mean

ABDM — Ayushman Bharat Digital Mission. The overall national digital-health ecosystem.  
NHA — National Health Authority. The body implementing ABDM.  
ABHA — Ayushman Bharat Health Account. A person’s unique health identity in the ABDM ecosystem. The ABHA Number is a 14-digit unique number.  
ABHA Address — A health-data communication/address identity associated with ABDM services. It is used in workflows such as login, linking/discovery of records and consent-based exchange. Do not treat it as the same thing as the 14-digit ABHA Number.  
HPR — Healthcare Professionals Registry. A registry for healthcare professionals.  
HFR — Health Facility Registry. A registry for health facilities such as hospitals, clinics, laboratories and other eligible facilities.  
PHR — Personal Health Record. Patient-facing functionality that lets an individual discover, link, view and manage health records and consents. The defining idea is that the individual controls access.  
HIP — Health Information Provider. An entity/system that creates or holds health information and can share it digitally using compliant software.  
HIU — Health Information User. An entity/system that requests and views a person’s health information with the person’s informed consent.  
Care Context — A logical grouping that tells the ecosystem which records belong to a particular episode or context of care.  
Consent Manager / Consent Artefact — The consent system records what data may be shared, with whom, for what purpose and within what scope. The consent artefact is machine-readable.  
FHIR — Fast Healthcare Interoperability Resources, the HL7 standard used by ABDM to structure exchangeable healthcare information.  
EMR — Electronic Medical Record. The clinical record used by the provider/system that generated it.  
EHR — Electronic Health Record. A broader longitudinal view of health information that can span multiple encounters and sources.

## 

## 

## 

## 4\. ABHA is an identity — not the medical record itself

A common misunderstanding is: “If the patient has ABHA, the government must already have all of the patient’s medical records.” That is not the correct mental model.

WRONG mental model:

ABHA \---\> one national database containing every prescription/report

BETTER mental model:

ABHA \---\> identifies the person

             |

             \+---- record at Hospital A

             \+---- report at Lab B

             \+---- prescription at Clinic C

ABDM helps these systems discover/link/share permitted information.

The records remain with the participating systems that hold them.

## 5\. What is a care context?

A patient can generate many records over time. ABDM needs a way to understand which records belong together. A care context is that grouping.

Patient: Priya

Care Context 001

  Antenatal consultation

  \+-- history

  \+-- examination

  \+-- diagnosis

  \+-- prescription

Care Context 002

  Ultrasound / diagnostic episode

  \+-- order

  \+-- report

Care Context 003

  Admission for delivery

  \+-- admission record

  \+-- procedures

  \+-- discharge summary

Tinytums should therefore think in terms of Patient \-\> Encounter/Episode \-\> Care Context \-\> Clinical Records, rather than storing unrelated PDFs with no clinical relationship.

## 6\. The simplest record-generation flow

Imagine a mother visiting a doctor using Tinytums.

Mother / Patient

      |

      v

Doctor at Hospital

      |

      v

Tinytums

      |

      \+-- creates encounter

      \+-- creates structured clinical record

      \+-- stores the record for the provider

      \+-- associates record with the correct patient

      \+-- groups relevant records into a care context

      |

      v

ABDM-enabled workflow can link/share the record when appropriate

In this situation, the provider/Tinytums side is performing the role of a Health Information Provider (HIP) because it is the source/holder of the health record.

## 7\. What happens when another provider wants the record?

Now suppose the same patient visits another hospital. The second provider wants her previous records.

Hospital B / Doctor B

        |

        | requests permitted records

        v

       HIU

        |

        v

ABDM consent workflow

        |

        v

Patient reviews request

     /         \\

 APPROVE       DENY

    |

    v

valid consent

    |

    v

Hospital A / Tinytums as HIP

    |

    \+-- identify permitted records

    \+-- package in required interoperable format

    \+-- securely transmit

    |

    v

Hospital B / HIU receives authorized information

The second hospital does not obtain unrestricted access to everything. The sharing is governed by the consent scope and the applicable ABDM rules.

## 8\. What does consent actually mean?

Consent should be thought of as a precise permission, not a permanent “yes”. In an electronic sharing workflow, the request can define the purpose, the types of health information requested, the relevant historical period and the access/validity window.  
The patient should know what is being requested and should be able to approve or deny the request. ABDM’s health-data policy emphasizes informed, specific and withdrawable consent and patient control over further processing.

A useful mental model:

WHO wants data?

        \+

WHAT data?

        \+

WHY is it needed?

        \+

FOR WHAT PERIOD?

        \+

FOR HOW LONG may it be accessed?

        |

        v

Patient decision

        |

        v

Machine-readable consent

## 9\. HIP and HIU are roles, not necessarily two different companies

Tinytums may eventually perform both roles.

Tinytums

   |

   \+-- HIP role

   |     creates/holds records and shares authorized records

   |

   \+-- HIU role

         requests authorized records from other providers

Example:

A doctor creates today's prescription in Tinytums \-\> HIP side.

The same doctor requests an old discharge summary from another hospital \-\> HIU side.

## 10\. Where FHIR fits

Different hospital software products store data differently. One may call a field diagnosis\_text; another may store coded conditions in a separate table. ABDM needs a common language for exchange. That is where HL7 FHIR comes in.

Tinytums internal database

        |

        | mapping / adapter

        v

ABDM FHIR-compliant health record

        |

        v

secure exchange

        |

        v

Another ABDM-compatible system

        |

        v

its own internal representation

Important developer lesson: Tinytums does not need to make its entire internal database identical to FHIR. It needs a clean internal clinical model plus a well-designed interoperability layer that can map to and from the required ABDM FHIR profiles.

## 11\. Mother and child are related — but they are not the same record

This matters enormously for Tinytums. Maternal and child care are clinically connected, but the mother and the child are separate persons with separate health records and identity lifecycles.

Mother

  |

  \+-- mother's demographics

  \+-- pregnancy records

  \+-- mother's diagnoses / medicines

  |

  \+---- Guardian / relationship \----\> Child

                                      |

                                      \+-- child's demographics

                                      \+-- birth record

                                      \+-- growth

                                      \+-- vaccination

                                      \+-- illnesses / prescriptions

Do not build the child as merely a sub-section inside the mother’s patient record. Build a real relationship model so that guardian rights, child identity, future independence of the child’s record and consent rules can be handled properly.

## 12\. What ABDM means for Tinytums conceptually

Tinytums should be viewed as a clinical software platform that may participate in the ABDM ecosystem on behalf of healthcare providers and, later, possibly through patient-facing PHR-style functions.

                     Tinytums Platform

                           |

        \+------------------+------------------+

        |                  |                  |

   Mother / Patient     Doctor App       Institution App

        |                  |                  |

        \+------------------+------------------+

                           |

                    Tinytums backend

                           |

          \+----------------+----------------+

          |                |                |

       Clinical         Consent /        ABDM

       records          audit layer      adapter

                                           |

                                  \+--------+--------+

                                  |                 |

                                 HIP               HIU

# PART B — BASIC DEVELOPER GUIDE: HOW TO BUILD FROM DAY ONE

## 13\. The core development principle

Do not build Tinytums as “a normal app first” and plan to bolt privacy, multi-institution access control and ABDM onto it later. Those concerns affect identity, data ownership, record structure, auditability and APIs. The correct strategy is to make the core architecture ABDM-ready without trying to implement every ABDM API in V1.

## 14\. Recommended high-level architecture

Mobile / Web Frontends

   |-- Mother / Patient

   |-- Doctor

   |-- Institution Admin

   |

   v

Application API / Backend

   |

   \+-- Authentication & session management

   \+-- Authorization / role-based access

   \+-- Patient & guardian service

   \+-- Professional & facility service

   \+-- Encounter / clinical-record service

   \+-- Consent service

   \+-- Audit service

   |

   v

Primary clinical database

   |

   \+-- structured clinical data

   \+-- document/file references

   \+-- version history

   \+-- tenant/institution ownership

   |

   v

Interoperability / ABDM Adapter Layer

   |

   \+-- external identifiers

   \+-- FHIR mapping

   \+-- ABDM API clients

   \+-- consent / HIP / HIU workflows

   |

   v

ABDM Sandbox / Production ecosystem

The key architectural choice is the separate ABDM Adapter Layer. This prevents your clinical database and business logic from becoming tightly coupled to one version of an external API.

## 15\. Core objects Tinytums should have from the beginning

At minimum, design clear objects/entities for the following. These are not the final ABDM integration matrix; they are the internal building blocks that will make later mapping possible.  
Person — the human being. Use an internal Tinytums identifier that exists independently of ABHA.  
Patient Profile — patient-specific demographic/clinical administrative details.  
Guardian / Relationship — mother-child, parent-child, caregiver, nominee or other legally relevant relationship. Store relationship status and its lifecycle explicitly.  
Healthcare Professional — doctor or other professional using Tinytums. Keep Tinytums identity separate from external registry identifiers.  
Facility / Institution — hospital, clinic, laboratory or organization. Every record/action should be attributable to the correct tenant/facility.  
Encounter — a real clinical interaction: OPD visit, teleconsultation, admission, discharge episode, etc.  
Care Context — logical grouping used for records that belong together and later need ABDM linkage/sharing.  
Clinical Record — observations, diagnoses, prescriptions, investigation orders/results, notes, discharge summaries and other structured records.  
External Identifier — ABHA Number, ABHA Address, HPR ID, HFR ID and future external identifiers should be stored as verified external identifiers, not used as the only internal primary key.  
Consent — store the purpose, scope, source, status, timestamps/lifecycle, subject and requester/provider relationships.  
Audit Event — who accessed/created/changed/shared what, when, from which context and for what action.

## 16\. Identity: do not use ABHA as your database primary key

Tinytums should create its own stable internal IDs. ABHA-related identifiers should be attached as external identifiers after the relevant verification/linking workflow.

Tinytums internal patient\_id \= PT\_100928

        |

        \+-- ABHA Number     \= external identifier

        \+-- ABHA Address    \= external identifier

        \+-- phone number    \= contact attribute

        \+-- hospital MRN    \= facility-specific identifier

Never make the entire database depend on:

patient\_id \== ABHA Number

Why? Because patients may first enter Tinytums without an ABHA-linked workflow, identifiers can have different verification states, and internal application integrity should not depend on a single external system.

## 17\. Multi-institution access control must be designed before features

Tinytums is intended for institutions where multiple doctors and care-team members may work. Therefore, authorization must answer two separate questions: “Who is this user?” and “What are they allowed to see/do in this institution and for this patient?”

Login identity

     |

     v

User

     |

     \+-- role: doctor / nurse / admin / etc.

     \+-- institution membership

     \+-- assigned care team

     \+-- specific permissions

     |

     v

Authorization decision

     |

     \+-- may view?

     \+-- may edit?

     \+-- may prescribe?

     \+-- may share?

     \+-- may export?

Institution A must not accidentally gain access to Institution B’s records simply because the same doctor, phone number or patient exists in both systems.

## 18\. Clinical records should be structured, attributable and versioned

Avoid designing the entire clinical system as free-text notes plus uploaded PDFs. PDFs can remain useful, but core data should be structured enough to support clinical workflows and interoperability.  
Each clinically important record should know: patient, encounter/care context, author, facility, creation time, status, version/amendment history and the structured clinical content.  
For medico-legal and audit reasons, “edit” should not silently erase history. Prefer amendments/versioning where clinically appropriate.

## 19\. Consent must be its own data model

Do not implement one checkbox called “I agree to everything”. Tinytums will eventually have multiple very different permissions and processing purposes.

Different concepts that should NOT be collapsed into one checkbox:

clinical care processing

        |

ABDM record-sharing consent

        |

research participation

        |

product analytics

        |

marketing / promotional communication

        |

optional AI or secondary processing

Each may require a different purpose, notice and legal/consent treatment.

The detailed legal mapping will come in the later integration matrix, but the software should be capable of representing separate permissions from day one.

## 20\. Audit logging is a product feature, not an afterthought

For sensitive health data, the team should be able to answer: Who opened this patient? Who changed this prescription? Who exported a report? Who initiated a sharing request? Which facility was the user acting for?  
Create an audit-event model early. Keep it tamper-resistant, access-controlled and useful for investigations. Do not dump full clinical notes, access tokens or secrets into ordinary application logs.

## 21\. Security baseline the developers should assume

The detailed security controls will later be mapped to current ABDM and legal requirements. As a baseline architecture, developers should already assume:  
• encryption in transit for all sensitive traffic;  
• encryption at rest for sensitive databases and object storage;  
• secure secrets/key management;  
• least-privilege permissions;  
• strong authentication and protected administrative access;  
• tenant isolation;  
• secure backups and tested recovery;  
• rate limiting and abuse protection;  
• vulnerability and dependency management;  
• separate development/test/sandbox/production environments;  
• no real patient data in casual development or demo environments unless specifically approved and protected;  
• careful log redaction so passwords, tokens, ABHA authentication secrets and unnecessary health data do not appear in logs.

## 22\. Keep ABDM integration behind an adapter

Do not scatter ABDM API calls throughout controllers and UI code. Create a dedicated integration layer.

Tinytums domain model

      |

      v

ABDM Adapter

      |

      \+-- identity / ABHA workflows

      \+-- care-context linking

      \+-- HIP workflows

      \+-- HIU workflows

      \+-- consent workflow

      \+-- FHIR serialization / validation

      \+-- external API error handling

      |

      v

ABDM

This lets the team update an API version, retry logic or FHIR mapping without rewriting the clinical application.

## 23\. FHIR strategy: internal model first, mapping second

The team should understand FHIR early, but should not blindly turn the entire Tinytums database into a copy of FHIR JSON. Keep a clean domain model that suits the product and create explicit mappings to the required ABDM FHIR profiles.  
For each exchangeable record type later, the integration matrix should define: Tinytums object \-\> required FHIR profile \-\> coding/value-set requirements \-\> mandatory fields \-\> validation \-\> HIP/HIU workflow.

## 24\. Maternal-child design rules

Because Tinytums focuses on maternal and child health, developers should follow these rules from the first schema design:  
• mother and child are separate Person/Patient entities;  
• pregnancy is not the child’s identity;  
• create explicit guardian/relationship records;  
• keep maternal records and child records clinically linkable but separately governed;  
• allow relationship/guardian permissions to change over time;  
• do not copy all maternal data into the child’s record;  
• do not assume the mother’s ABHA or consent automatically substitutes for the child’s identity/consent workflow.

## 25\. Suggested development order

A practical sequence that minimizes rework:  
Step 1 — Build the product’s internal identity model: users, persons, patients, professionals, facilities and institution membership.  
Step 2 — Build encounters, care episodes/care contexts and structured clinical records.  
Step 3 — Add authorization, tenant isolation and care-team permissions.  
Step 4 — Add audit events, record versioning and secure logging.  
Step 5 — Add the consent/permission model even before full ABDM connectivity.  
Step 6 — Build the interoperability adapter and FHIR mapping/validation layer.  
Step 7 — Integrate the required ABHA/identity workflows in the ABDM Sandbox.  
Step 8 — Add HIP workflows for linking/sharing records generated by Tinytums.  
Step 9 — Add HIU workflows when Tinytums doctors need to request outside records.  
Step 10 — Complete current sandbox-exit, security and production-onboarding requirements before production connectivity.

## 26\. What NOT to do

Do not:  
• assume ABHA is a centralized medical-record database;  
• use ABHA Number as Tinytums’ only patient identifier;  
• use one universal consent checkbox for every purpose;  
• make child records merely a nested part of the mother’s record;  
• allow cross-institution visibility by default;  
• put raw patient data, authentication tokens or secrets into normal application logs;  
• tightly couple the clinical database to a particular ABDM API version;  
• store only PDFs when important clinical information can be structured;  
• silently overwrite clinically important records without version/amendment history;  
• build production ABDM integration from old blogs, screenshots or third-party tutorials when an official current specification is available.

## 27\. A developer’s mental checklist for every new feature

Whenever the team adds a feature, ask:  
1\. Whose data is this?  
2\. Which institution owns/holds this clinical record?  
3\. Which encounter/care context does it belong to?  
4\. Who created it?  
5\. Who may view or change it?  
6\. Does the action require a specific consent or permission?  
7\. What must be written to the audit trail?  
8\. Is any external identifier involved and has it been verified?  
9\. Could this object later need to map to an ABDM FHIR profile?  
10\. Are we exposing more data than is necessary for the purpose?

## 28\. The full Tinytums mental model

ABHA tells us WHO the patient is in ABDM.

HPR tells us WHO the healthcare professional is.

HFR tells us WHICH registered facility is involved.

Tinytums tells us:

  WHAT happened clinically,

  WHERE it happened,

  WHO authored it,

  WHICH encounter/care context it belongs to,

  WHO may access it,

  and HOW it is stored and audited.

HIP \= Tinytums/provider sharing records it holds.

HIU \= Tinytums/provider requesting permitted outside records.

Consent \= the patient's authorization for the defined sharing.

FHIR \= the common language used to exchange the record.

ABDM \= the trust/interoperability framework joining these pieces.

# OFFICIAL REFERENCE STARTING POINTS

Use official/current documentation during implementation. Useful starting points:  
1\. ABDM official portal — https://abdm.gov.in/  
2\. ABDM Health Data Management Policy — https://abdm.gov.in/static/media/health\_management\_policy\_bac9429a79.80f74bc3e039c00acd4f.pdf  
3\. ABDM / MoHFW digital-systems overview — https://ahpr.abdm.gov.in/about  
4\. NRCeS ABDM FHIR Implementation Guide — https://www.nrces.in/ndhm/fhir/r4/  
5\. ABDM Sandbox — https://sandbox.abdm.gov.in/

Source note: This document summarizes the stable conceptual model from official ABDM/NHA materials. For coding and production onboarding, current Sandbox specifications and the current published FHIR guide take precedence over this orientation document.  
