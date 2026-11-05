#	Field	Draft Underwriter Consideration
1	First Claim Date	Confirm the available claim history goes back far enough to cover the applicable underwriting lookback period.
2	Last Claim Date	Identify the most recent claim activity and determine whether it falls within the applicable lookback period.
3	Total Claims	Use only as a volume indicator to understand how much claim history requires review; do not infer risk from count alone.
4	Total Claim Records / Unique Claim Count	Identify the number of distinct claim events that need review; multiple claim lines may belong to the same claim.
5	Total Application Conditions	If greater than zero, prioritize those application-related conditions for review, but do not limit review only to those conditions.
6	Current Application Conditions List	Use as the starting condition list; compare each condition against the applicant’s answers, lookback rules, and claim evidence, while still checking for additional relevant conditions not listed here.
7	Account / Member Number	Use as the trusted member-level join/filter key to ensure all claims and evidence belong to the correct applicant/case.
8	Member First / Last Name	Use for identity validation only; do not use as an underwriting decision factor.
9	Member DOB	Use for identity validation and matching records to the correct member; not a standalone medical finding.
10	Plan Product	Use as coverage/application context, especially for plan changes or prior coverage; do not infer a medical decision from plan type alone.
11	Claim Number	Group related claim lines into the same claim/event and retain it as an evidence reference for the underwriter.
12	Claim Line Number	Identify the exact diagnosis/procedure line within a claim so the specific supporting evidence can be traced and cited.
13	CPT Code	Use to determine what service/procedure occurred—such as office visit, MRI, injection, surgery, or treatment—and distinguish diagnostic testing from actual treatment/management.
14	CPT Description	Provide human-readable context for the CPT service and help determine whether the claim represents testing, follow-up, treatment, or another type of encounter.
15	ICD Code	Use as the primary structured signal for a possible diagnosis/condition; map it to underwriting conditions and lookback rules, but do not treat one code alone as confirmed disease without context.
16	ICD Description	Use as the human-readable diagnosis description for review and summary; interpret together with ICD code, CPT/service context, frequency, and supporting records.
17	Incur / Service Date	Determine whether the evidence falls inside the applicable lookback period and establish chronology/repeated occurrences of the condition.
18	POS – Place of Service	Use the care setting—office, inpatient, ER, outpatient, etc.—as supporting context for the encounter; never make the decision from POS alone.


Application condition / UW consideration
        ↓
ICD → What condition may be present?
        ↓
Service date → Is it inside lookback?
        ↓
CPT → What was actually done?
        ↓
POS → Where did the encounter happen?
        ↓
Frequency → One isolated occurrence or repeated evidence?
        ↓
Medical/office notes → Confirmed diagnosis or only investigation?
        ↓
Result:
Confirmed / Supporting evidence
Possible – needs review
Diagnostic/testing only
Outside lookback
Contradiction
