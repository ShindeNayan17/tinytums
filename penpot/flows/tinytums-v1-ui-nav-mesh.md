# TinyTums V1 — full screen navigation mesh

From [`tinytums-v1-ui-map.json`](tinytums-v1-ui-map.json). **160 screens**, **201 actions**.

If preview is slow, paste [`tinytums-v1-ui-nav-mesh.mmd`](tinytums-v1-ui-nav-mesh.mmd) into [mermaid.live](https://mermaid.live).

Legend: edge = tap/action. `[xd]` = iOS ↔ web. `?` = showIf. `skip` = skipIf.

## New screens (Sep 2026)

29 screens added (14 + 6 extended scope + 9 new):

### Mother Home boards with enriched dashboards (p02)
Four themed dashboards with cream/paper/rose/teal and aligned peach secondary chips:
- `iosDashHero` — iOS / Dashboard hero (pregnant) — chips: Weight, Glucose
- `iosDashTtc` — iOS / Dashboard TTC — chips: Preconception, Meal ideas
- `iosDashPp` — iOS / Dashboard postpartum — chips: Aarav home, Postpartum; Family planning in Care network card
- `iosDashLoss` — iOS / Dashboard pregnancy loss (NEW) — chips: Sensitive details, Find care

### Same-page gate boards (p02)
Penpot Play uses same-page navigate-to; gates link to canonical destinations on other pages:
- `iosPreconceptionGate` — iOS / Preconception · gate → iosTtc (p03)
- `iosMealIdeasGate` — iOS / Meal ideas · gate → iosMealSuggest (p03)
- `iosPostpartumGate` — iOS / Postpartum hub · gate → iosPphub (p03)
- `iosChildHomeGate` — iOS / Child home · gate → iosChildHome (p05)
- `iosWeightGate` — iOS / Weight · gate → iosWeight (p04)
- `iosGlucoseGate` — iOS / Glucose · gate → iosGlucose (p04)
- `iosFindCareGate` — iOS / Find care · gate → iosSearchH (p06)

### Postpartum hub restacked (p03)
- `iosRecoverySymptoms` — iOS / Recovery & symptoms (NEW)
- Cards: Recovery & symptoms, Nutrition & weight, Menstrual return, Breastfeeding support, Contraception / future planning (68px tall, 12px gap)

### Prior screens (14 + 6 extended scope)
- `webInstCreate` — Web / Institution create (p10)
- `webStaffAccept` — Web / Staff invite accept (p08)
- `iosEntitlement` — iOS / Subscription entitlement (p02)
- `iosTeleInCall` — iOS / Teleconsult in-call (p06)
- `webTeleInCall` — Web / Teleconsult in-call (p09)
- `iosCgSections` — iOS / Caregiver sections (p06)
- `iosTwinDelivery` — iOS / Twin delivery → children (p02)
- `iosCorrectedAge` — iOS / Corrected age (p05)
- `iosBreastfeed` — iOS / Breastfeeding log (p03)
- `iosFamilyPlan` — iOS / Family planning (p03)
- `iosSensitiveOutcome` — iOS / Sensitive outcome (p02)
- `webWardTransfer` — Web / Ward transfer (p10)
- `webReadmission` — Web / Readmission (p10)
- `iosObgyPrompt` — iOS / Primary OBGY prompt (p02)

### Extended scope (badges: future/aiAssist/regulatoryHold/amber)
- `iosPregSummaryGen` — iOS / Pregnancy summary (generated) (p03) — F-037 — aiAssist
- `iosMealSuggest` — iOS / Meal suggestions (p03) — F-038 — future
- `iosMicroTrack` — iOS / Micronutrient tracking (p04) — F-039 — future
- `iosAiHold` — iOS / Regulated AI hold (p03) — F-045 — regulatoryHold
- `webAiHold` — Web / Regulated AI hold (p08) — F-045 — regulatoryHold
- `iosBloodLabs` — iOS / Blood investigations tracker (p04) — F-047 — amber

## Gap finder

### No inbound (hard to reach unless tab/deep link)
- `iosSplash` — iOS / Splash
- `iosCgInviteExpired` — iOS / Caregiver invite expired
- `webLogin` — Web / Login
- `webAdmin` — Web / Admin staff
- `webRbacMatrix` — Web / RBAC matrix
- `abhaPrivacySplit` — iOS / ABDM vs privacy
- `webHpr` — Web / Staff HPR
- `webInstCreate` — Web / Institution create (via webDashAdmin)

### No outbound (dead ends — OK if terminal)
- `iosTasks` — iOS / Tasks due
- `iosNotifications` — iOS / Notifications
- `iosPrivacy` — iOS / Privacy consent
- `iosPrivacyAbdm` — iOS / Privacy + ABDM row
- `iosLogout` — iOS / Logout confirm
- `iosPphub` — iOS / Postpartum hub
- `iosPeriod` — iOS / Period tracking
- `iosLogBpSheet` — iOS / Log BP sheet
- `iosSymptoms` — iOS / Symptoms
- `iosReportView` — iOS / Report view
- `iosLogWeightSheet` — iOS / Log weight sheet
- `iosLogGlucoseSheet` — iOS / Log glucose sheet
- `iosGrowth` — iOS / Growth
- `iosVax` — iOS / Vaccines
- `iosCorrectedAge` — iOS / Corrected age
- `iosBreastfeed` — iOS / Breastfeeding log
- `iosFamilyPlan` — iOS / Family planning
- `iosSensitiveOutcome` — iOS / Sensitive outcome
- `webInstCreate` — Web / Institution create
- `webWardTransfer` — Web / Ward transfer
- `webReadmission` — Web / Readmission
- `iosPregSummaryGen` — iOS / Pregnancy summary (generated)
- `iosMealSuggest` — iOS / Meal suggestions
- `iosMicroTrack` — iOS / Micronutrient tracking
- `iosBloodLabs` — iOS / Blood investigations tracker
- `iosPlay` — iOS / Activities
- `iosAfter` — iOS / After visit
- `iosCgInviteExpired` — iOS / Caregiver invite expired
- `iosShareProfessional` — iOS / Share with doctor
- `iosAlliedSearch` — iOS / Allied search
- `iosReschedule` — iOS / Reschedule appointment
- `iosAdmissionTeam` — iOS / Admission care team
- `cgDeny` — iOS / Caregiver edit denied
- `webAccessDenied` — Web / Access denied
- `webStaffPending` — Web / Staff pending
- `webPediatrician` — Web / Pediatrician workspace
- `webEnc01` — Web / Enc §01 Patient ID
- `webEnc02` — Web / Enc §02 Chief complaints
- `webEnc03` — Web / Enc §03 HPI
- `webEnc04` — Web / Enc §04 Past history
- `webEnc05` — Web / Enc §05 Meds allergy
- `webEnc06` — Web / Enc §06 Personal social
- `webEnc07` — Web / Enc §07 Family history
- `webEnc08` — Web / Enc §08 Special history
- `webEnc09` — Web / Enc §09 General exam
- `webEnc10` — Web / Enc §10 Systemic exam
- `webEnc11` — Web / Enc §11 Clinical summary
- `webEnc12` — Web / Enc §12 Provisional dx
- `webEnc13` — Web / Enc §13 Investigations
- `webEnc15` — Web / Enc §15 Advice
- `webEnc16` — Web / Enc §16 Referral
- `webEnc17` — Web / Enc §17 Follow-up
- `webEnc18` — Web / Enc §18 Doctor auth
- `webClinicianInbox` — Web / Clinician inbox
- `webTeleJoin` — Web / Teleconsult join
- `webViewSource` — Web / View source
- `webCorrectionQueue` — Web / Correction queue
- `webAdmissionChart` — Web / Admission chart
- `webJunior` — Web / Junior doctor
- `webDashObgy` — Web / Dash OBGY
- `webDashNurse` — Web / Dash Nurse
- `webDashJunior` — Web / Dash Junior
- `webDashPedia` — Web / Dash Pediatrician
- `webDashAllied` — Web / Dash Allied
- `webDashAdmin` — Web / Dash Admin
- `webInviteStaff` — Web / Invite staff
- `webVerifyQueue` — Web / Verify staff queue
- `webAuditLog` — Web / Audit log
- `webMonitoringPlan` — Web / Monitoring plan
- `webAlliedWs` — Web / Allied workspace
- `abhaCard` — iOS / ABHA card
- `abhaChild` — iOS / Child ABHA
- `abhaRecordView` — iOS / View linked record
- `abhaRevoke` — iOS / Revoke consent
- `abhaPrivacySplit` — iOS / ABDM vs privacy
- `webHfr` — Web / Facility HFR
- `webHpr` — Web / Staff HPR
- `webLinkPatientAbha` — Web / Link patient ABHA
- `webCareContexts` — Web / Care contexts
- `webHipQr` — Web / HIP QR link token
- `webHipShare` — Web / HIP share status
- `webHiuGranted` — Web / HIU consent granted
- `webHiuDenied` — Web / HIU denied expired

### Isolated (no in and no out)
- `iosCgInviteExpired` — iOS / Caregiver invite expired
- `abhaPrivacySplit` — iOS / ABDM vs privacy
- `webHpr` — Web / Staff HPR

## Mesh

```mermaid
flowchart TB
  subgraph iOS_auth [iOS auth]
    iosSplash["Splash"]
    iosSignIn["Sign in"]
    iosOtp["OTP verify"]
    iosAccount["Create account"]
    iosEmailOptional["Email optional"]
    iosState["State picker"]
  end
  subgraph iOS_home [iOS home]
    iosDashHero["Dashboard hero"]
    iosDashTtc["Dashboard TTC"]
    iosDashPp["Dashboard postpartum"]
    iosDashLoss["Dashboard pregnancy loss"]
    iosNoObgy["No primary OBGY"]
    iosAccess["Clinic access"]
    iosAccessDenied["Access denied"]
    iosEmptyHome["Empty home"]
    iosPregnancyLoss["Pregnancy loss state"]
    iosDeliveryChild["Delivery → child"]
    iosTasks["Tasks due"]
    iosNotifications["Notifications"]
  end
  subgraph iOS_gates [iOS gates p02]
    iosPreconceptionGate["Preconception · gate"]
    iosMealIdeasGate["Meal ideas · gate"]
    iosPostpartumGate["Postpartum hub · gate"]
    iosChildHomeGate["Child home · gate"]
    iosWeightGate["Weight · gate"]
    iosGlucoseGate["Glucose · gate"]
    iosFindCareGate["Find care · gate"]
  end
  subgraph iOS_you [iOS you]
    iosYou["You hub"]
    iosProfile["Profile"]
    iosLock["Verified lock"]
    iosPrivacy["Privacy consent"]
    iosPrivacyAbdm["Privacy + ABDM row"]
    iosCorrection["Correction request"]
    iosLogout["Logout confirm"]
    iosTtc["Preconception"]
    iosPreg["Pregnancy episode"]
    iosPphub["Postpartum hub"]
    iosRecoverySymptoms["Recovery & symptoms"]
    iosPeriod["Period tracking"]
  end
  subgraph iOS_track [iOS track]
    iosWeight["Weight"]
    iosBp["BP"]
    iosLogBpSheet["Log BP sheet"]
    iosUploadReport["Upload report"]
    iosGlucose["Glucose"]
    iosPndIntro["PND intro"]
    iosPndQ["PND questions"]
    iosPndResult["PND result"]
    iosSymptoms["Symptoms"]
    iosReports["Reports library"]
    iosReportView["Report view"]
    iosLogWeightSheet["Log weight sheet"]
    iosLogGlucoseSheet["Log glucose sheet"]
  end
  subgraph iOS_child [iOS child]
    iosKids["Children list"]
    iosAddChild["Add child"]
    iosChildHome["Child home"]
    iosGrowth["Growth"]
    iosVax["Vaccines"]
    iosMiles["Milestones"]
    iosPlay["Activities"]
  end
  subgraph iOS_care [iOS care]
    iosSearchH["Search hospital"]
    iosSearchD["Search doctor"]
    iosDocInst["Doctor at institution"]
    iosInvite["Invite doctor"]
    iosInviteSent["Invite sent"]
    iosBook["Book appointment"]
    iosApptsList["Appointments list"]
    iosPacket["Pre-visit packet"]
    iosMsg["Messages"]
    iosTele["Teleconsult"]
    iosAfter["After visit"]
    iosCgShare["Caregiver share"]
    iosCgList["Caregivers list"]
    iosCgInvite["Invite caregiver"]
    iosCgInviteSent["Caregiver invite sent"]
    iosCgInviteExpired["Caregiver invite expired"]
    iosShareProfessional["Share with doctor"]
    iosHospital["Hospital page"]
    iosDoctorProfile["Doctor profile"]
    iosAlliedSearch["Allied search"]
    iosReschedule["Reschedule appointment"]
    iosAdmissionTeam["Admission care team"]
  end
  subgraph iOS_cg [iOS cg]
    cgLogin["Caregiver login"]
    cgOtp["Caregiver OTP"]
    cgHome["Caregiver home"]
    cgDeny["Caregiver edit denied"]
  end
  subgraph iOS_abha [iOS abha]
    abhaHub["ABHA hub"]
    abhaCreate["Create ABHA"]
    abhaLink["Link ABHA"]
    abhaKycOtp["ABHA OTP KYC"]
    abhaLinked["ABHA linked"]
    abhaCard["ABHA card"]
    abhaSkip["Skip ABHA"]
    abhaChild["Child ABHA"]
    abhaDiscover["Discover records"]
    abhaLinkContexts["Link care contexts"]
    abhaRecordsList["Linked records list"]
    abhaRecordView["View linked record"]
    abhaConsentReq["Consent request"]
    abhaConsentDecision["Consent approve deny"]
    abhaMyConsents["My consents"]
    abhaRevoke["Revoke consent"]
    abhaPrivacySplit["ABDM vs privacy"]
  end
  subgraph Web_auth [Web auth]
    webLogin["Login"]
    webStaffOtp["Staff OTP"]
    webWorkspacePicker["Workspace picker"]
    webWorkspaceSkip["Workspace skip"]
    webStaffPending["Staff pending"]
  end
  subgraph Web_ops [Web ops]
    webOps["Ops dashboard"]
    webAccessDenied["Access denied"]
    webPediatrician["Pediatrician workspace"]
    webMaster["Patient master"]
    webChart["Patient chart"]
    webMonitoringPlan["Monitoring plan"]
    webAlliedWs["Allied workspace"]
  end
  subgraph Web_enc [Web enc]
    webSum["Factual summary"]
    webEnc["Encounter form"]
    webEnc01["Enc §01 Patient ID"]
    webEnc02["Enc §02 Chief complaints"]
    webEnc03["Enc §03 HPI"]
    webEnc04["Enc §04 Past history"]
    webEnc05["Enc §05 Meds allergy"]
    webEnc06["Enc §06 Personal social"]
    webEnc07["Enc §07 Family history"]
    webEnc08["Enc §08 Special history"]
    webEnc09["Enc §09 General exam"]
    webEnc10["Enc §10 Systemic exam"]
    webEnc11["Enc §11 Clinical summary"]
    webEnc12["Enc §12 Provisional dx"]
    webEnc13["Enc §13 Investigations"]
    webEnc14["Enc §14 Treatment"]
    webEnc15["Enc §15 Advice"]
    webEnc16["Enc §16 Referral"]
    webEnc17["Enc §17 Follow-up"]
    webEnc18["Enc §18 Doctor auth"]
    webVerify["Verify field"]
    webRx["Prescription"]
    webClinicianInbox["Clinician inbox"]
    webTeleJoin["Teleconsult join"]
    webViewSource["View source"]
    webCorrectionQueue["Correction queue"]
    webFollowUp["Follow-up book"]
  end
  subgraph Web_admit [Web admit]
    webAdmit["Admit"]
    webAdmissionChart["Admission chart"]
    webTeam["Care team assign"]
    webDischarge["Discharge"]
    webNurse["Nurse role"]
    webJunior["Junior doctor"]
    webAdmin["Admin staff"]
    webInviteStaff["Invite staff"]
    webVerifyQueue["Verify staff queue"]
    webDischargeSummary["Discharge summary"]
    webPlannedAdmit["Planned admission"]
    webAuditLog["Audit log"]
  end
  subgraph Web_rbac [Web rbac]
    webRbacMatrix["RBAC matrix"]
    webDashObgy["Dash OBGY"]
    webDashNurse["Dash Nurse"]
    webDashJunior["Dash Junior"]
    webDashPedia["Dash Pediatrician"]
    webDashAllied["Dash Allied"]
    webDashAdmin["Dash Admin"]
  end
  subgraph Web_abdm [Web abdm]
    webHfr["Facility HFR"]
    webHpr["Staff HPR"]
    webLinkPatientAbha["Link patient ABHA"]
    webCareContexts["Care contexts"]
    webHipQr["HIP QR link token"]
    webHipShare["HIP share status"]
    webHiuRequest["HIU request records"]
    webHiuPending["HIU consent pending"]
    webHiuGranted["HIU consent granted"]
    webHiuDenied["HIU denied expired"]
    webHiuPickPerson["HIU pick person"]
  end

  iosSplash -->|"Get started"| iosAccount
  iosSplash -->|"Sign in"| iosSignIn
  iosSignIn -->|"Send OTP"| iosOtp
  iosAccount -->|"Continue"| iosOtp
  iosOtp -->|"New user"| iosEmailOptional
  iosOtp -->|"Verify skip"| iosState
  iosEmailOptional -->|"Skip or save"| iosState
  iosOtp -->|"Optional ABHA setup"| abhaHub
  abhaSkip -->|"Continue to app"| iosState
  abhaHub -->|"Create ABHA"| abhaCreate
  abhaHub -->|"Link existing"| abhaLink
  abhaHub -->|"Skip for now"| abhaSkip
  abhaCreate -->|"Continue"| abhaKycOtp
  abhaLink -->|"Continue"| abhaKycOtp
  abhaKycOtp -->|"Verify ABHA"| abhaLinked
  abhaLinked -->|"View card"| abhaCard
  abhaLinked -->|"Discover records"| abhaDiscover
  abhaDiscover -->|"Select facility"| abhaLinkContexts
  abhaLinkContexts -->|"Link selected"| abhaRecordsList
  abhaRecordsList -->|"Open record"| abhaRecordView
  abhaConsentReq -->|"Review"| abhaConsentDecision
  abhaConsentDecision -->|"Approve or deny"| abhaMyConsents
  abhaMyConsents -->|"Revoke"| abhaRevoke
  abhaLinked -->|"Child ABHA"| abhaChild
  webHiuRequest -->|"Before send"| webHiuPickPerson
  webHiuPickPerson -->|"Send consent request"| webHiuPending
  webHiuPending -->|"Patient notified [xd]"| abhaConsentReq
  abhaConsentDecision -->|"Approve"| webHiuGranted
  abhaConsentDecision -->|"Deny"| webHiuDenied
  webEnc -->|"HIP share after encounter ?"| webHipShare
  iosState -->|"Pregnant + child"| iosDashHero
  iosState -->|"Trying to conceive"| iosDashTtc
  iosState -->|"Postpartum / child"| iosDashPp
  iosState -->|"Pregnancy loss"| iosPregnancyLoss
  iosDashHero -->|"No primary OBGY ?"| iosNoObgy
  iosDashHero -->|"You / access"| iosAccess
  iosDashHero -->|"No entitlement"| iosAccessDenied
  iosAccessDenied -->|"Request granted"| iosAccess
  iosDashHero -->|"First-time user"| iosEmptyHome
  iosDashHero -->|"Pregnancy card"| iosPreg
  iosDashHero -->|"Child card"| iosChildHome
  iosDashHero -->|"Log BP"| iosBp
  iosBp -->|"Quick log sheet"| iosLogBpSheet
  iosWeight -->|"Log reading"| iosLogWeightSheet
  iosGlucose -->|"Log reading"| iosLogGlucoseSheet
  iosReports -->|"Upload"| iosUploadReport
  iosReports -->|"Open report"| iosReportView
  iosUploadReport -->|"Saved to library"| iosReports
  iosDashHero -->|"Visit card"| iosBook
  iosDashHero -->|"Appointments"| iosApptsList
  iosDashHero -->|"Tasks due"| iosTasks
  iosDashHero -->|"Notifications bell"| iosNotifications
  iosDashHero -->|"Log symptom"| iosSymptoms
  iosDashHero -->|"Reports"| iosReports
  iosDashTtc -->|"Preconception hub"| iosTtc
  iosTtc -->|"Period tracking"| iosPeriod
  iosDashPp -->|"Postpartum hub"| iosPphub
  iosDashPp -->|"Mood screening"| iosPndIntro
  iosPreg -->|"Delivery recorded"| iosDeliveryChild
  iosNoObgy -->|"Find doctor"| iosSearchH
  iosNoObgy -->|"Invite mine"| iosInvite
  iosProfile -->|"Verified field"| iosLock
  iosProfile -->|"Privacy"| iosPrivacy
  iosProfile -->|"ABDM row"| iosPrivacyAbdm
  iosLock -->|"Request correction"| iosCorrection
  iosProfile -->|"Sign out"| iosLogout
  iosWeight -->|"Home"| iosDashHero
  iosBp -->|"After log"| iosBook
  iosPndIntro -->|"Begin"| iosPndQ
  iosPndQ -->|"Next / complete"| iosPndResult
  iosPndResult -->|"Share with clinician"| iosMsg
  iosKids -->|"Open Aarav"| iosChildHome
  iosChildHome -->|"Growth"| iosGrowth
  iosChildHome -->|"Vaccines"| iosVax
  iosChildHome -->|"Milestones"| iosMiles
  iosChildHome -->|"Activities"| iosPlay
  iosSearchH -->|"Open hospital"| iosHospital
  iosHospital -->|"Pick doctor"| iosDoctorProfile
  iosSearchH -->|"Pick hospital then doctor"| iosDocInst
  iosSearchH -->|"Search by doctor"| iosSearchD
  iosSearchH -->|"Allied professionals"| iosAlliedSearch
  iosSearchD -->|"Pick Doctor X @ Institution Y"| iosDocInst
  iosDoctorProfile -->|"Choose location"| iosDocInst
  iosDocInst -->|"Connect / book"| iosBook
  iosDocInst -->|"Manage sharing"| iosShareProfessional
  iosApptsList -->|"Reschedule or cancel"| iosReschedule
  iosInvite -->|"Send invite"| iosInviteSent
  iosInviteSent -->|"Done"| iosDashHero
  iosBook -->|"Confirm slot"| iosPacket
  iosBook -->|"Teleconsult type"| iosTele
  iosPacket -->|"After visit"| iosAfter
  iosMsg -->|"Clinician asks visit"| iosBook
  iosTele -->|"Encounter complete"| iosAfter
  iosDashHero -->|"Tab Child"| iosKids
  iosDashHero -->|"Tab Care"| iosSearchH
  iosDashHero -->|"Tab You"| iosYou
  iosKids -->|"Tab Home"| iosDashHero
  iosSearchH -->|"Tab Home"| iosDashHero
  iosYou -->|"Tab Home"| iosDashHero
  iosYou -->|"Tab Care"| iosSearchH
  iosYou -->|"Tab Child"| iosKids
  iosYou -->|"Maternal profile"| iosProfile
  iosYou -->|"Clinic access"| iosAccess
  iosYou -->|"Caregivers"| iosCgList
  iosYou -->|"Privacy"| iosPrivacy
  iosYou -->|"Health ID / ABHA"| abhaHub
  iosYou -->|"Sign out"| iosLogout
  iosKids -->|"Add child"| iosAddChild
  iosAddChild -->|"Create child profile"| iosChildHome
  iosDeliveryChild -->|"Create child profile"| iosAddChild
  iosEmptyHome -->|"Set up profile"| iosYou
  iosChildHome -->|"Share with caregiver"| iosCgList
  iosCgList -->|"Invite caregiver"| iosCgInvite
  iosCgList -->|"Open Rahul"| iosCgShare
  iosCgInvite -->|"Send invite"| iosCgInviteSent
  iosCgInviteSent -->|"Done"| iosCgList
  iosCgInviteSent -->|"Caregiver opens SMS link"| cgLogin
  iosCgShare -->|"Manage caregivers"| iosCgList
  cgLogin -->|"Send OTP"| cgOtp
  cgOtp -->|"Continue skip"| cgHome
  cgHome -->|"Tap edit"| cgDeny
  webLogin -->|"Send OTP"| webStaffOtp
  webStaffOtp -->|"Verify ?"| webWorkspacePicker
  webStaffOtp -->|"Verify skip"| webWorkspaceSkip
  webWorkspaceSkip -->|"Auto enter"| webOps
  webWorkspacePicker -->|"Select Role @ Institution"| webOps
  webWorkspacePicker -->|"OBGY @ Sunrise"| webDashObgy
  webWorkspacePicker -->|"Junior @ Sunrise"| webDashJunior
  webWorkspacePicker -->|"Nurse @ Sunrise"| webDashNurse
  webWorkspacePicker -->|"Pediatrician @ Sunrise"| webDashPedia
  webWorkspacePicker -->|"Allied @ Sunrise"| webDashAllied
  webWorkspacePicker -->|"Admin @ Sunrise"| webDashAdmin
  webRbacMatrix -->|"Open OBGY dash"| webDashObgy
  webRbacMatrix -->|"Open Junior dash"| webDashJunior
  webRbacMatrix -->|"Open Nurse dash"| webDashNurse
  webRbacMatrix -->|"Open Pedia dash"| webDashPedia
  webRbacMatrix -->|"Open Allied dash"| webDashAllied
  webRbacMatrix -->|"Open Admin dash"| webDashAdmin
  webOps -->|"Header switch"| webWorkspacePicker
  webStaffOtp -->|"Pending approval ?"| webStaffPending
  webOps -->|"Patients"| webMaster
  webOps -->|"Open queue patient"| webSum
  webOps -->|"Admissions"| webAdmit
  webOps -->|"Inbox"| webClinicianInbox
  webOps -->|"Teleconsult"| webTeleJoin
  webOps -->|"Pediatric role workspace"| webPediatrician
  webMaster -->|"Open Priya"| webChart
  webChart -->|"Not on care team"| webAccessDenied
  webChart -->|"Factual summary"| webSum
  webChart -->|"Set home monitoring"| webMonitoringPlan
  webSum -->|"View source"| webViewSource
  iosCorrection -->|"Clinician notified [xd]"| webCorrectionQueue
  webChart -->|"Link ABHA"| webLinkPatientAbha
  webChart -->|"Switch to child person"| iosChildHome
  webSum -->|"Start encounter"| webEnc
  webEnc -->|"§1 Patient ID"| webEnc01
  webEnc -->|"§2 Chief complaints"| webEnc02
  webEnc -->|"§3 HPI"| webEnc03
  webEnc -->|"§4 Past history"| webEnc04
  webEnc -->|"§5 Meds & allergy"| webEnc05
  webEnc -->|"§6 Personal & social"| webEnc06
  webEnc -->|"§7 Family history"| webEnc07
  webEnc -->|"§8 Special history"| webEnc08
  webEnc -->|"§9 General exam"| webEnc09
  webEnc -->|"§10 Systemic exam"| webEnc10
  webEnc -->|"§11 Clinical summary"| webEnc11
  webEnc -->|"§12 Provisional dx"| webEnc12
  webEnc -->|"§13 Investigations"| webEnc13
  webEnc -->|"§14 Treatment"| webEnc14
  webEnc -->|"§15 Advice"| webEnc15
  webEnc -->|"§16 Referral"| webEnc16
  webEnc -->|"§17 Follow-up"| webEnc17
  webEnc -->|"§18 Doctor auth"| webEnc18
  webEnc14 -->|"Open prescription"| webRx
  webEnc -->|"Review field"| webVerify
  webEnc -->|"Treatment shortcut"| webRx
  webVerify -->|"Verify and lock"| webRx
  webRx -->|"Mother notified"| iosAfter
  webRx -->|"Book follow-up"| webFollowUp
  webFollowUp -->|"Mother confirms slot [xd]"| iosBook
  webAdmit -->|"Open inpatient chart"| webAdmissionChart
  webAdmit -->|"Assign staff"| webTeam
  webTeam -->|"Nurse Patel context"| webNurse
  webTeam -->|"Junior Shah context"| webJunior
  webNurse -->|"Enter vitals only"| webChart
  webAdmit -->|"Plan discharge"| webDischarge
  webAdmit -->|"From appointment"| webPlannedAdmit
  webPlannedAdmit -->|"Mother sees team [xd]"| iosAdmissionTeam
  webDischarge -->|"Write summary"| webDischargeSummary
  webDischargeSummary -->|"Mother can view [xd]"| iosAfter
  webDischarge -->|"Temp access ends"| webChart
  webAdmin -->|"Invite named staff"| webTeam
  webAdmin -->|"Invite staff"| webInviteStaff
  webAdmin -->|"Verification queue"| webVerifyQueue
  webAdmin -->|"Audit log"| webAuditLog
  webOps -->|"Allied workspace"| webAlliedWs
  webAdmin -->|"HFR settings"| webHfr
  webAdmin -->|"HIP QR"| webHipQr
  webChart -->|"Care contexts"| webCareContexts
  webChart -->|"Request outside records"| webHiuRequest
  iosInvite -->|"Lead sent (legacy edge)"| iosDashHero

  %% New: Pregnancy loss dashboard + gate boards (Sep 2026)
  iosPregnancyLoss -->|"Continue to home"| iosDashLoss
  iosDashLoss -->|"Sensitive details chip"| iosSensitiveOutcome
  iosDashLoss -->|"Find care chip"| iosFindCareGate

  %% Dashboard chip → gate edges
  iosDashHero -->|"Weight chip"| iosWeightGate
  iosDashHero -->|"Glucose chip"| iosGlucoseGate
  iosDashTtc -->|"Preconception chip"| iosPreconceptionGate
  iosDashTtc -->|"Meal ideas chip"| iosMealIdeasGate
  iosDashPp -->|"Aarav home chip"| iosChildHomeGate
  iosDashPp -->|"Postpartum chip"| iosPostpartumGate

  %% Gate → canonical destination edges
  iosPreconceptionGate -->|"Back"| iosDashTtc
  iosPreconceptionGate -->|"Continue"| iosTtc
  iosMealIdeasGate -->|"Back"| iosDashTtc
  iosMealIdeasGate -->|"Continue"| iosMealSuggest
  iosPostpartumGate -->|"Back"| iosDashPp
  iosPostpartumGate -->|"Continue"| iosPphub
  iosChildHomeGate -->|"Back"| iosDashPp
  iosChildHomeGate -->|"Continue"| iosChildHome
  iosWeightGate -->|"Back"| iosDashHero
  iosWeightGate -->|"Continue"| iosWeight
  iosGlucoseGate -->|"Back"| iosDashHero
  iosGlucoseGate -->|"Continue"| iosGlucose
  iosFindCareGate -->|"Back"| iosDashLoss
  iosFindCareGate -->|"Continue"| iosSearchH

  %% Postpartum hub restacked cards
  iosPphub -->|"Recovery & symptoms"| iosRecoverySymptoms
  iosPphub -->|"Nutrition & weight"| iosMealSuggest
  iosPphub -->|"Menstrual return"| iosTtc
```
