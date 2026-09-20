# Purpose and Scope

This document is the current source of truth for Tinytums V1. It converts founder discussions into a product specification that can be used by founders, designers, developers, clinical partners, regulatory advisers, and pilot teams. Unresolved items are marked TBD rather than guessed. Confidential founder/commercial details that have not been disclosed remain intentionally outside this document.

## Product Thesis

Tinytums is a longitudinal maternal-and-child health platform whose central goal is to extend evidence-based care from the clinic into the home. It is designed around continuous, structured information flow between the mother and her healthcare professionals, while preserving clinician responsibility for diagnosis and treatment.

## Primary Users

The two primary user groups are Mother and Healthcare Professionals. A mother is the owner of the consumer account and may have one or more reproductive journeys, pregnancies, and child profiles. Healthcare professionals may include OBGYs, pediatricians, physiotherapists, lactation/breastfeeding consultants, dietitians/nutrition professionals, junior doctors/residents, nurses, and other approved maternal-child professionals.

## Core V1 Journeys

V1 supports preconception / trying to conceive, active pregnancy, postpartum maternal health, and child health from birth through age seven at the same time. Tinytums must support a mother who is trying to conceive, a primigravida, a mother with an existing child who is also pregnant, a mother with several children, and multiple pregnancy. The data model should also allow sensitive handling of pregnancy loss, stillbirth, neonatal loss, and future pregnancy planning without inappropriate reminders.

## Unified Mother Dashboard

The mother sees one fluid home dashboard rather than separate apps or disconnected journeys. The dashboard adapts to her current state and can simultaneously surface her own health, active pregnancy, existing children, connected care team, upcoming appointments, measurements/tasks due, reports, vaccinations, developmental milestones, and selected education or care activities.

## Maternal Longitudinal Profile

The maternal master profile persists beyond pregnancy. It may include identity and contact basics, height, baseline and longitudinal weight, blood group/Rh status, allergies, chronic conditions, long-term medicines, obstetric history, nutrition information, menstrual tracking, preconception planning, postpartum recovery, mental-health screening, and future pregnancy planning. Dynamic measurements such as weight remain longitudinal rather than being represented by one static field.

## Pregnancy Episode

Each pregnancy is a separate clinical episode linked to the maternal master profile. Pregnancy-specific information may include LMP, EDD, gestational age, pregnancy number, obstetric status, fetal information, investigations, symptoms, current diagnoses entered by clinicians, doctor-prescribed monitoring such as BP or blood glucose, pregnancy weight trend, appointments, reports, and pregnancy-related care records. An unborn baby is represented as an upcoming baby/pregnancy entity until delivery.

## Delivery Transition

At delivery, the pregnancy episode transitions into two linked longitudinal pathways: the mother's postpartum/ongoing health profile and one or more child profiles. The maternal profile continues permanently. The child profile begins at birth. For twins or higher-order multiple pregnancies, more than one child profile is created from the pregnancy.

## Postnatal and Postpartum Model

Tinytums should preserve standard scientific terminology while using product phases that meet user needs. The first 42 days after birth are treated as the standard postnatal period. The product may present a broader postpartum care journey through approximately 12 weeks, followed by ongoing maternal health rather than ending maternal care. Postpartum features may include nutrition, weight, symptoms, recovery, menstrual return, contraception/future pregnancy planning, mental-health screening, breastfeeding-related support, and clinician follow-up.

## Maternal Mental Health

Questionnaires for postnatal depression or related conditions are screening tools, not diagnoses. V1 may administer validated screening questionnaires and store/share the responses and scores, but diagnosis and management remain with a healthcare professional. Any future automated interpretation that materially triages, diagnoses, or assigns urgency must pass the regulatory gate before rollout.

## Child Profile: Birth to Age Seven

Each child has an independent longitudinal profile linked to the mother. V1 should support growth tracking, vaccination records and reminders, pediatric clinic summaries, illnesses/records, prescriptions/reports as applicable, developmental milestone tracking, upcoming milestones, and age-appropriate development-promoting activities. Growth-chart implementation should be evidence-based and use appropriate standards for age and context.

## Developmental Milestones

The app may show age-appropriate expected milestones and allow the mother to record whether a milestone has been observed. Upcoming milestones can be shown in advance. The dashboard may indicate that a milestone has not yet been recorded and encourage discussion with the pediatrician. V1 should avoid declaring developmental delay from a simple checklist. Formal screening instruments and automated clinical interpretation are separate future functions. Corrected age must be considered for relevant preterm children when milestone timing is displayed.

## Development-Promoting Activities

Tinytums may provide simple age-appropriate activities that support development, such as communication, recognition, play, movement, colours, objects, numbers, language, and other evidence-based early-childhood activities. These should be framed as development-promoting activities rather than diagnostic tests unless a validated screening workflow is intentionally introduced later.

## Data State Model

Clinically relevant information may be entered by the mother when onboarding or between visits. Until reviewed, such information is marked self-reported/unverified. An authorised clinician can review and confirm the field, converting it to clinician-verified status. Once verified, the mother cannot directly overwrite the verified clinical value. She may request correction or add new information for clinician review. The system should preserve an audit trail showing who entered, reviewed, corrected, or verified important clinical information.

## Examples of Clinician-Verified Fields

Examples may include blood group/Rh status, clinically relevant allergies, gravida/para and obstetric history, confirmed EDD, chronic diagnoses, significant previous pregnancy complications, important investigation results, and doctor-defined monitoring plans. The final set of lockable fields should be defined with clinical and UX review. Dynamic home measurements remain longitudinal entries even when baseline values are clinician-verified.

## Home Tracking

V1 may allow mothers to record doctor-requested or useful measurements such as weight, blood pressure, blood glucose, and other selected vital/health parameters. The product may display the values, dates, trends, counts, ranges, and missing entries. In V1 it must not automatically declare a measurement clinically abnormal, assign urgency, predict deterioration, diagnose disease, or recommend treatment.

## Generated Clinical Summary

Before or during a visit, Tinytums can generate a factual summary of information entered since the previous clinical review. Examples include number of BP readings, recorded ranges, weight change, glucose entries, symptoms reported, reports uploaded, questionnaires completed, appointments, or adherence entries. The doctor must be able to drill down from the summary to the original source data. The summary is not a diagnosis and should not hide or replace source records.

## V1 Regulatory Gate

V1 is intentionally designed as a non-device, doctor-led digital health and telemedicine platform. The software may store, organise, display, summarise, and transmit health information and facilitate clinician review. The following automated functions are excluded from V1 commercial activation: clinical abnormality flags, urgency labels, automated triage, disease diagnosis, deterioration prediction, risk stratification intended to drive care, treatment recommendations, medicine changes, or automated clinical counselling. Any proposed feature performing those functions must be routed to the regulatory gate.

## V2+ Clinical Intelligence

A later rollout may analyse patient-entered and clinical data to identify information requiring attention, prioritise cases, detect concerning patterns, or support clinical decisions. These features are likely to require formal medical-device software analysis, CDSCO classification, quality management, technical validation, clinical validation, and post-market planning. The regulated module should be architecturally separable from non-device Tinytums functions where practical.

## Teleconsultation

Teleconsultation is part of V1. Tinytums may facilitate complaint submission, messaging, appointment scheduling, document/report sharing, audio/video consultation where implemented, and doctor-issued advice/prescriptions. The healthcare professional remains responsible for determining whether teleconsultation is appropriate, whether an in-person examination is required, and what diagnosis or treatment is appropriate.

## Primary OBGY Relationship

A primary OBGY is strongly encouraged for an active pregnancy. Tinytums remains functional if no primary OBGY is connected, but the app should repeatedly and respectfully prompt the user to find a doctor on Tinytums or invite her existing doctor. If the connected primary OBGY/institution is a subscribing Tinytums customer, the mother receives enhanced access included through that relationship.

## Healthcare Professional Discovery

A mother can search by hospital/clinic and then select a doctor practising there, or search by doctor and choose a listed institution/practice location for that doctor. The connection is specific to Doctor X at Institution Y. Search ranking logic is TBD. Public professional profiles should use verified professional identity information and institution/practice context.

## Invite My Doctor Lead Flow

If the user's doctor is not present on Tinytums, the mother can submit basic information such as clinician name, specialty, clinic/hospital, city, and contact information if known. This creates an internal clinician lead. Tinytums should not publish a professional profile solely from patient-submitted data. The team verifies the clinician and approaches them for onboarding.

## Institution-First Professional Model

Tinytums professional operations are institution-first. A hospital, maternity centre, or clinic has its own institutional account. In many private practices the owner and primary OBGY may be the same person. Professional staff operate using individual named accounts under the institution. Shared clinical logins/passwords are not acceptable.

## Professional Identity and Verification

Doctors may provide registration number and relevant professional/profile information, with Tinytums verifying registration status through the appropriate official registry. Claimed specialty/qualification data should be handled as a separate verified profile field where necessary. Physiotherapists, lactation professionals, dietitians, and other allied professionals are verified through a documented Tinytums manual verification process until a suitable authoritative registry/process is available for the relevant profession.

## Hospital / Clinician Dashboard

The professional dashboard is designed as a clinical operations and patient-management interface. It should show institution name and current clinician identity, today's total appointments, currently admitted patients, discharge planned, discharged today, upcoming admissions, appointment-time queue, patients seen today, access to the complete patient master database, an inpatient admissions area, diagnosis/care documentation entered by clinicians, teleconsultation workflows, and clinical care-team management.

## Patient Master Record

The institution should have access to an authorised master patient database for patients connected to or treated within that institution. Search and filters may include patient identity, pregnancy status/gestational age, appointment status, admission status, last review, upcoming appointment, and relevant operational fields. Exact filters and permissions are to be refined in design.

## Admission Episode

An admission creates a time-bounded institutional care episode. The hospital can assign authorised staff to the patient without requiring the mother to approve each individual staff member separately during that admission. Staff receive only role-appropriate access through their own accounts. Every material record entry or access-sensitive action should be attributable to an individual user.

## Clinical Care Team Roles

Role-based access control is required. A primary/consultant OBGY may have broad clinical access. Junior doctors/residents may have broad clinical access subject to institutional policy and supervision. Nurses may be able to view only the information required for their role and enter selected observations/vitals while being restricted from unrelated information such as certain laboratory data. Other roles receive tailored permissions. Exact permission matrices are TBD and should be configurable within safe bounds.

## Discharge Access

At discharge, temporary admission-team access ends or is materially reduced. Only individually connected healthcare professionals retain longitudinal access after discharge, and each professional sees only the information the mother has chosen to share with that professional. Institutional access and ongoing individual clinician access are separate relationships.

## External and Multidisciplinary Care

A mother can simultaneously connect to pediatricians, physiotherapists, lactation/breastfeeding consultants, dietitians/nutrition professionals, and other approved professionals. These professionals do not automatically receive the same access as the primary OBGY. The mother controls which relevant sections are shared with each ongoing professional.

## Family Caregiver Access

Family caregivers are separate from clinical care-team users. In V1, a caregiver may have mother-authorised read-only access on their own device to selected maternal or child information. Caregivers do not independently enter or edit health records. The mother can change or revoke caregiver access.

## Consent and Access Principle

Tinytums should follow minimum-necessary, purpose-appropriate sharing. The mother controls ongoing sharing with external/connected professionals and family caregivers. During an active hospital admission, the institution may assign authorised care-team members under the admission relationship. Access changes should be auditable and revocable where appropriate.

## Commercial Model

The current model is hybrid B2B2C plus freemium. A subscribing Primary OBGY/institution can enable enhanced access for mothers connected under that clinical relationship without labelling them as 'premium' users. If no subscribing primary OBGY is connected, the mother retains core functionality and may pay for selected advanced consumer features. Exact pricing and the detailed doctor-paid value proposition are confidential/TBD.

## Potential Enhanced Consumer Features

Examples under consideration include a generated current-pregnancy summary, advanced nutrition tools, meal suggestions, and micronutrient tracking. These features must remain within the V1 regulatory boundary unless separately reviewed. General education/personalisation should be distinguished from disease-specific clinical counselling or treatment recommendations.

## Pilot Strategy

The first real-world pilot will be in one Tier-2/Tier-3 Indian city rather than a national launch. Approximate target scale is 5-10 OBGYs with about 20-50 mothers each, producing roughly 100-500 mothers depending on recruitment. The pilot should include the multidisciplinary model from day one, including pediatricians and relevant allied professionals rather than testing only an OBGY workflow.

## Pilot Objectives

The pilot should measure whether mothers can use the product across different levels of health literacy, whether clinicians can efficiently review longitudinal information, whether the generated factual summary helps consultations, whether multidisciplinary sharing works safely, whether the hospital dashboard matches real operational workflows, whether teleconsultation is usable, and whether the commercial model produces willingness to continue.

## Evidence and Safety Principles

Tinytums should prefer guideline-based content and clearly distinguish education, self-tracking, screening, and clinical diagnosis. Source data should remain visible to clinicians. Patient-entered information should be labelled until verified. Clinical outputs created by professionals should remain identifiable as professional entries. Automated interpretation must not be added to V1 simply because it is technically easy.

## Product Architecture Principles

The system should be modular. Suggested domains include Identity and Accounts; Mother Master Profile; Reproductive Journey; Pregnancy Episode; Child Profile; Measurements and Tracking; Documents/Reports; Milestones and Vaccinations; Appointments; Teleconsultation; Messaging/Complaints; Institution; Professional Directory; Admission Episodes; Clinical Care Teams; Consent/Permissions; Audit Trail; Summaries; Subscription/Entitlements; and a future Regulated Clinical Intelligence module.

## Auditability

Important actions should have timestamps and actor identity. Examples include entering a vital, verifying a clinical field, uploading or reviewing a report, changing permissions, assigning an inpatient care-team role, creating a diagnosis/clinical note, issuing a prescription, and changing verified data. Audit requirements should be specified with legal/security advisers before production deployment.

## Data Provenance

Every clinically relevant datum should ideally retain provenance such as self-reported, clinician-entered, clinician-verified, uploaded-document-derived, institution-entered, or future device/API-derived. Generated summaries must reference or link back to source data.

## Out of Scope / Not Yet Finalised

Search-result ranking, exact UI design, final paywall feature list, exact institutional pricing, detailed doctor value proposition, precise allied-professional verification criteria, final role-permission matrix, pilot city, participating hospitals, exact teleconsultation technical stack, ABDM integration timing, detailed legal documents, detailed data-retention rules, and V2 clinical-intelligence intended use remain TBD.

## Definition of V1 Success

A successful V1 should prove that Tinytums can become a trusted longitudinal care layer connecting home and clinic for maternal and child health, without relying on autonomous clinical AI. It should demonstrate useful tracking, structured records, verified clinical data, factual summaries, teleconsultation, multidisciplinary sharing, institution workflows, admission-role access, and sustained mother/clinician engagement.

## Change-Control Rule

Any future product request that introduces automated clinical interpretation must be reviewed against the V1 regulatory boundary before development or release. The Product Master should be updated whenever founders approve a material change in user roles, access, clinical function, business model, pilot design, or regulatory position.  
