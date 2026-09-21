# TinyTums V1 — design flow (Mermaid)

Source of truth for screen IDs and edges: [`tinytums-v1-ui-map.json`](tinytums-v1-ui-map.json).  
Boards live in Penpot. This file is the repo copy of how those screens connect.

## 1. System map

```mermaid
flowchart LR
  subgraph iosApp [iOS]
    Mother
    Caregiver
  end
  subgraph webPortal [Web]
    Doctor
    Nurse
    Junior
    Admin
  end
  Mother -->|shareConsent_readOnly| Caregiver
  Mother -->|"DoctorX_at_InstitutionY"| Doctor
  Admin -->|namedStaff| Doctor
  Admin -->|namedStaff| Nurse
  Admin -->|namedStaff| Junior
```

## 2. Penpot page map

```mermaid
flowchart TB
  p00[00 Cover + map]
  p01[01 Design system]
  p02[02 iOS Onboarding + Home]
  p03[03 iOS Mother journeys]
  p04[04 iOS Track + mind]
  p05[05 iOS Child]
  p06[06 iOS Care network]
  p07[07 iOS Caregiver]
  p08[08 Web Ops + patients]
  p09[09 Web Encounter]
  p09b[09b Encounter sections]
  p10[10 Web Admission + roles]
  p11[11 iOS ABDM / ABHA]
  p12[12 Web ABDM HIP / HIU]
  p13[13 Walk A mother]
  p14[14 Walk B clinician]
  p15[15 Walk C ABDM consent]
  p00 --> p01
  p01 --> p02
  p02 --> p03
  p03 --> p04
  p04 --> p05
  p05 --> p06
  p06 --> p07
  p07 --> p08
  p08 --> p09
  p09 --> p09b
  p09b --> p10
  p10 --> p11
  p11 --> p12
  p12 --> p13
  p13 --> p14
  p14 --> p15
```

## 3. Mother iOS — auth and onboarding

```mermaid
flowchart TD
  iosSplash[Splash] --> iosAccount[Create account phone first]
  iosSplash --> iosSignIn[Sign in phone]
  iosSignIn --> iosOtp[TinyTums OTP]
  iosAccount --> iosOtp
  iosOtp --> iosEmailOptional[Email optional]
  iosEmailOptional --> iosState[Current state picker]
  iosOtp -->|skipIf savedLifeState| iosDashHero[Dashboard hero]
  iosOtp -->|optional| abhaHub[ABHA hub F-046]
  abhaHub --> abhaSkip[Skip ABHA]
  abhaSkip --> iosState
  iosAccount --> iosState
  iosState -->|TTC| iosDashTtc[Dashboard TTC]
  iosState -->|pregnant_plus_child| iosDashHero[Dashboard hero]
  iosState -->|postpartum| iosDashPp[Dashboard postpartum]
  iosDashHero -->|no_OBGY| iosNoObgy[No primary OBGY]
  iosDashHero --> iosAccess[Clinic access F-036]
  iosNoObgy -->|Find doctor| iosSearchH[Search hospital]
  iosNoObgy -->|Invite mine| iosInvite[Invite doctor lead]
  iosDashTtc --> iosTtc[Preconception hub]
  iosDashPp --> iosPphub[Postpartum hub]
  iosDashHero --> iosPreg[Pregnancy episode]
  iosDashHero --> iosChildHome[Child home]
```

## 4. Mother record, tracking, mind

```mermaid
flowchart TD
  iosProfile[Maternal profile] --> iosLock[Verified lock + history]
  iosProfile --> iosPrivacy[Split consent purposes]
  iosDashHero[Dashboard hero] --> iosWeight[Weight trend]
  iosDashHero --> iosBp[BP trend]
  iosDashHero --> iosGlucose[Glucose trend]
  iosDashHero --> iosSymptoms[Symptoms log]
  iosDashHero --> iosReports[Reports library]
  iosReports --> iosReportView[Report view PDF]
  iosReports --> iosUploadReport[Upload report]
  iosWeight --> iosLogWeightSheet[Log weight sheet]
  iosGlucose --> iosLogGlucoseSheet[Log glucose sheet]
  iosDashHero --> iosTasks[Tasks due]
  iosTtc[Preconception hub] --> iosPeriod[Period tracking]
  iosDashPp[Postpartum dashboard] --> iosPndIntro[PND intro]
  iosPndIntro --> iosPndQ[PND questions]
  iosPndQ --> iosPndResult[Score recorded]
  iosPndResult -->|share| iosMsg[Messages]
```

## 5. Child profile — own person

```mermaid
flowchart TD
  iosKids[Children list twins] --> iosAddChild[Add child]
  iosKids --> iosChildHome[Child home Aarav]
  iosDeliveryChild[Delivery to child] --> iosAddChild
  iosChildHome --> iosGrowth[Growth chart]
  iosChildHome --> iosVax[Vaccines]
  iosChildHome --> iosMiles[Milestones + corrected age]
  iosChildHome --> iosPlay[Play activities]
```

## 6. Care network and visit

```mermaid
flowchart TD
  iosSearchH[Search hospital] --> iosHospital[Hospital page]
  iosHospital --> iosDoctorProfile[Doctor profile]
  iosSearchH --> iosDocInst[Doctor X at Institution Y]
  iosSearchH --> iosSearchD[Search doctor]
  iosSearchH --> iosAlliedSearch[Allied search]
  iosSearchD --> iosDocInst
  iosDocInst --> iosShareProfessional[Share sections with doctor]
  iosDocInst --> iosBook[Book visit or teleconsult]
  iosApptsList[Appointments list] --> iosReschedule[Reschedule or cancel]
  iosInvite[Invite doctor] -->|lead_not_profile| iosDashHero[Dashboard]
  iosBook -->|in_person| iosPacket[Pre-visit packet]
  iosBook -->|teleconsult| iosTele[Teleconsult]
  iosPacket --> iosAfter[After-visit Rx]
  iosTele --> iosAfter
  iosMsg[Messages] --> iosBook
  iosYou[You hub] --> iosCgList[Caregivers list]
  iosCgList --> iosCgInvite[Invite caregiver]
  iosCgInvite --> iosCgInviteSent[Invite sent]
  iosCgInviteSent --> cgLogin[Caregiver login]
  iosCgList --> iosCgShare[Share permissions]
  iosCgShare --> iosCgList
```

## 7. Caregiver iOS

```mermaid
flowchart TD
  cgLogin[Caregiver login phone] --> cgOtp[Caregiver OTP]
  cgOtp --> cgHome[Read-only home]
  cgOtp -->|skipIf invite expired| iosCgInviteExpired[Invite expired]
  cgHome -->|tap_edit| cgDeny[Edit denied]
```

## 8. Web portal — auth workspace ops

```mermaid
flowchart TD
  webLogin[Staff phone login] --> webStaffOtp[Staff OTP]
  webStaffOtp -->|showIf 2+ workspaces| webWorkspacePicker[Role at Institution]
  webStaffOtp -->|skipIf one workspace| webWorkspaceSkip[Auto-selected]
  webWorkspacePicker --> webOps[Ops dashboard]
  webWorkspaceSkip --> webOps
  webOps -->|header switch| webWorkspacePicker
  webStaffOtp -->|showIf pending| webStaffPending[Staff pending block]
  webOps --> webMaster[Patient master]
  webMaster --> webChart[Longitudinal chart]
  webChart -->|switch_person| childPerson[Child Aarav record]
  webOps -->|queue_patient| webSum[Factual summary]
  webChart --> webMonitoringPlan[Home monitoring plan]
```

## 9. Encounter and verification

```mermaid
flowchart TD
  webSum[Factual summary] --> webViewSource[View source drill-down]
  webSum --> webEnc[Encounter TOC 18 sections]
  iosCorrection[Correction request] --> webCorrectionQueue[Clinician queue]
  webEnc --> webEnc01[Section boards on p09b]
  webEnc --> webVerify[Verify and lock field]
  webEnc --> webRx[Named prescription]
  webVerify --> webRx
  webRx --> iosAfter[Mother after-visit]
```

## 10. Admission and roles

```mermaid
flowchart TD
  webAdmit[Create admission episode] --> webPlannedAdmit[Planned from appointment]
  webPlannedAdmit --> iosAdmissionTeam[Mother sees care team]
  webAdmit --> webTeam[Assign named care team]
  webTeam --> webNurse[Nurse vitals only]
  webTeam --> webJunior[Junior + supervision banner]
  webAdmit --> webDischarge[Close episode]
  webDischarge --> webDischargeSummary[Discharge summary doc]
  webDischargeSummary --> iosAfter[Mother after-visit]
  webDischarge -->|temp_access_ends| webChart[Ongoing only if mother shares]
  webAdmin[Admin staff verify] --> webInviteStaff[Invite named staff]
  webAdmin --> webVerifyQueue[Staff verification queue]
  webAdmin --> webAuditLog[Audit log]
  webOps --> webAlliedWs[Allied workspace]
  webRx[Prescription] --> webFollowUp[Book follow-up]
  webWorkspacePicker[Role at Institution] --> webRbacMatrix[RBAC matrix]
  webRbacMatrix --> webDashObgy[Dash OBGY]
  webRbacMatrix --> webDashNurse[Dash Nurse vitals only]
  webRbacMatrix --> webDashJunior[Dash Junior supervised]
  webRbacMatrix --> webDashPedia[Dash Pediatrician]
  webRbacMatrix --> webDashAllied[Dash Allied sections]
  webRbacMatrix --> webDashAdmin[Dash Admin no chart]
```

## 11. Prototype walks in Penpot Play

```mermaid
flowchart LR
  subgraph walkA [Walk A mother]
    iosDashHero[Dashboard hero] --> iosBp[BP] --> iosBook[Book] --> iosPacket[Pre-visit packet]
  end
```

```mermaid
flowchart LR
  subgraph walkB [Walk B clinician]
    webOps[Ops dashboard] --> webSum[Factual summary] --> webEnc[Encounter] --> webVerify[Verify] --> webRx[Rx]
  end
```

```mermaid
flowchart LR
  subgraph walkC [Walk C ABDM consent]
    iosOtp[OTP] --> abhaHub[ABHA hub] --> abhaLink[Link ABHA] --> abhaKycOtp[ABHA OTP] --> abhaLinked[Linked]
    abhaLinked --> abhaConsentReq[Consent request] --> abhaConsentDecision[Approve] --> webHiuGranted[HIU view]
  end
```

## 12. ABDM iOS — PHR consent

```mermaid
flowchart TD
  abhaHub[ABHA hub TT-ID primary] --> abhaCreate[Create ABHA]
  abhaHub --> abhaLink[Link existing]
  abhaHub --> abhaSkip[Skip for now]
  abhaCreate --> abhaKycOtp[Gov ABHA OTP]
  abhaLink --> abhaKycOtp
  abhaKycOtp --> abhaLinked[External IDs verified]
  abhaLinked --> abhaDiscover[Discover HIP]
  abhaDiscover --> abhaLinkContexts[Link care contexts]
  abhaLinkContexts --> abhaRecordsList[Linked records list]
  abhaConsentReq[Consent request] --> abhaConsentDecision[Approve or deny]
  abhaMyConsents[My consents] --> abhaRevoke[Revoke]
  abhaLinked --> abhaChild[Child ABHA own person]
```

## 13. ABDM web — HIP HIU

```mermaid
flowchart TD
  webHfr[Facility HFR] --> webHipQr[HIP QR token]
  webHpr[Staff HPR] --> webChart[Patient chart]
  webLinkPatientAbha[Link patient ABHA optional] --> webCareContexts[Care contexts]
  webHiuRequest[HIU request] --> webHiuPickPerson[Mother vs child]
  webHiuPickPerson --> webHiuPending[Consent pending]
  webHiuPending --> abhaConsentReq[Patient mobile]
  abhaConsentDecision[Patient decision] --> webHiuGranted[Granted view]
  abhaConsentDecision --> webHiuDenied[Denied expired]
  webEnc[Encounter] --> webHipShare[HIP share status]
```

## 14. New flows (Sep 2026)

### Institution + staff onboarding
```mermaid
flowchart TD
  webDashAdmin[Dash Admin] --> webInstCreate[Institution create]
  webInviteStaff[Invite staff] -->|cross-device| webStaffAccept[Staff invite accept]
  webStaffAccept --> webStaffOtp[Staff OTP]
```

### Subscription entitlement
```mermaid
flowchart TD
  iosAccess[Clinic access] --> iosEntitlement[Subscription entitlement]
  iosAccessDenied[Access denied] --> iosEntitlement
  iosYou[You hub] --> iosEntitlement
```

### Teleconsult in-call
```mermaid
flowchart TD
  iosTele[Teleconsult] --> iosTeleInCall[Teleconsult in-call]
  iosTeleInCall --> iosAfter[After visit]
  webTeleJoin[Teleconsult join] --> webTeleInCall[Web Teleconsult in-call]
  webTeleInCall --> webRx[Prescription]
```

### Caregiver granular sections
```mermaid
flowchart TD
  iosCgShare[Caregiver share] --> iosCgSections[Caregiver sections picker]
  iosCgSections --> iosCgShare
```

### Twin delivery + corrected age
```mermaid
flowchart TD
  iosDeliveryChild[Delivery → child] --> iosTwinDelivery[Twin delivery → children]
  iosTwinDelivery --> iosKids[Children list]
  iosMiles[Milestones] --> iosCorrectedAge[Corrected age]
```

### Postpartum breastfeeding + family planning
```mermaid
flowchart TD
  iosPphub[Postpartum hub] --> iosBreastfeed[Breastfeeding log]
  iosPphub --> iosFamilyPlan[Family planning]
```

### Sensitive outcome
```mermaid
flowchart TD
  iosPregnancyLoss[Pregnancy loss state] --> iosSensitiveOutcome[Sensitive outcome]
  iosState[State picker] --> iosSensitiveOutcome
```

### Ward transfer + readmission
```mermaid
flowchart TD
  webAdmit[Admit] --> webWardTransfer[Ward transfer]
  webAdmissionChart[Admission chart] --> webWardTransfer
  webAdmit --> webReadmission[Readmission]
```

### Primary OBGY soft prompt
```mermaid
flowchart TD
  iosDashHero[Dashboard hero] -->|"showIf noPrimaryObgy"| iosObgyPrompt[Primary OBGY prompt]
  iosObgyPrompt --> iosSearchH[Search hospital]
  iosObgyPrompt --> iosInvite[Invite doctor]
  iosObgyPrompt --> iosDashHero
```

## 15. Mother Home dashboards with themed chips (Sep 2026)

Four enriched dashboards with cream/paper/rose/teal theme and aligned peach secondary chips:

### Dashboard variants
```mermaid
flowchart TD
  iosState[State picker] --> iosDashHero[Dashboard hero - pregnant]
  iosState --> iosDashTtc[Dashboard TTC]
  iosState --> iosDashPp[Dashboard postpartum]
  iosState --> iosPregnancyLoss[Pregnancy loss state]
  iosPregnancyLoss --> iosDashLoss[Dashboard pregnancy loss]
```

### Home chips → gate boards
Penpot cannot persist cross-page navigate-to. Home chips use same-page gate boards:

```mermaid
flowchart TD
  subgraph Dashboard_hero [Dashboard hero chips]
    iosDashHero[Dashboard hero] --> iosWeightGate[Weight · gate]
    iosDashHero --> iosGlucoseGate[Glucose · gate]
  end
  subgraph Dashboard_TTC [Dashboard TTC chips]
    iosDashTtc[Dashboard TTC] --> iosPreconceptionGate[Preconception · gate]
    iosDashTtc --> iosMealIdeasGate[Meal ideas · gate]
  end
  subgraph Dashboard_postpartum [Dashboard postpartum chips]
    iosDashPp[Dashboard postpartum] --> iosChildHomeGate[Child home · gate]
    iosDashPp --> iosPostpartumGate[Postpartum hub · gate]
  end
  subgraph Dashboard_loss [Dashboard pregnancy loss chips]
    iosDashLoss[Dashboard pregnancy loss] --> iosSensitiveOutcome[Sensitive outcome]
    iosDashLoss --> iosFindCareGate[Find care · gate]
  end
```

### Gate → canonical destination
```mermaid
flowchart LR
  iosPreconceptionGate[Preconception · gate] --> iosTtc[iOS / Preconception p03]
  iosMealIdeasGate[Meal ideas · gate] --> iosMealSuggest[iOS / Meal suggestions p03]
  iosPostpartumGate[Postpartum hub · gate] --> iosPphub[iOS / Postpartum hub p03]
  iosChildHomeGate[Child home · gate] --> iosChildHome[iOS / Child home p05]
  iosWeightGate[Weight · gate] --> iosWeight[iOS / Weight p04]
  iosGlucoseGate[Glucose · gate] --> iosGlucose[iOS / Glucose p04]
  iosFindCareGate[Find care · gate] --> iosSearchH[iOS / Search hospital p06]
```

## 16. Postpartum hub restacked (Sep 2026)

Cards evenly spaced (68px tall, 12px gap). Tap targets:

```mermaid
flowchart TD
  iosPphub[Postpartum hub] --> iosRecoverySymptoms[Recovery & symptoms]
  iosPphub --> iosMealSuggest[Nutrition & weight → Meal suggestions]
  iosPphub --> iosTtc[Menstrual return → Preconception]
  iosPphub --> iosBreastfeed[Breastfeeding support → Breastfeeding log]
  iosPphub --> iosFamilyPlan[Contraception / future planning → Family planning]
```

## 17. Extended scope (F-037, F-038, F-039, F-045, F-047)

Badges: `future` | `aiAssist` | `regulatoryHold` | `amber`

### Pregnancy summary (generated) — F-037
```mermaid
flowchart TD
  iosPreg[Pregnancy episode] --> iosPregSummaryGen["Pregnancy summary (generated) 🤖"]
  iosPphub[Postpartum hub] --> iosPregSummaryGen
  iosPregSummaryGen --> iosReportView[View source]
```

### Meal suggestions — F-038
```mermaid
flowchart TD
  iosTtc[Preconception] --> iosMealSuggest["Meal suggestions 🔮"]
  iosPphub[Postpartum hub] --> iosMealSuggest
```

### Micronutrient tracking — F-039
```mermaid
flowchart TD
  iosYou[You hub] --> iosMicroTrack["Micronutrient tracking 🔮"]
```

### Blood investigations tracker — F-047
```mermaid
flowchart TD
  iosReports[Reports library] --> iosBloodLabs["Blood labs tracker 🟡"]
  iosBloodLabs --> iosReportView[View source]
```

### Regulated AI hold gate — F-045
```mermaid
flowchart TD
  iosYou[You hub] --> iosAiHold["Regulated AI hold ⏸️"]
  iosAiHold --> iosYou
  webOps[Ops dashboard] --> webAiHold["Web Regulated AI hold ⏸️"]
  webAiHold --> webOps
```

## 18. V1 fence

```mermaid
flowchart LR
  v1[V1 allowed: store display trends factual_summary teleconsult consent verify]
  v2[V2 held: auto_flag triage diagnosis risk treatment]
  v1 -.->|regulatory_gate| v2
```
