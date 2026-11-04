# Product Requirements Document (PRD)

# TripWeaver AI

**AI-Powered Personalized Travel Planner & Coordinated Booking Platform**

| Document control | Value |
| --- | --- |
| Course | IBE160 — Programmering med KI, Autumn 2026 |
| Team | G103 — Team Alpha Omega |
| Version | **1.0 — Final** |
| Prepared | 4 November 2026 |
| Status | **Approved for project planning** |
| Product | **TripWeaver AI** |
| Primary source | [`productbrief2.md`](https://github.com/IBE160-2026/G103-berge-hagen-holmen-nguyen/blob/main/productbrief2.md) |
| Assessment reference | *Sensorveiledning IBE160 – Del 1, applikasjon og prosess* (7 pages) |
| Approval | **Approved 4 November 2026**; implementation scope, technology and integration decisions remain open where identified |

> **Document purpose.** This PRD translates the TripWeaver AI project brief into requirements that can be designed, built, tested, reviewed and traced to development evidence. The product brief sets the vision; this PRD proposes how to deliver and verify it. **TripWeaver AI—not SimpleTravel—is the product in scope.**
>
> 
> **Source distinction.** The product capabilities below are based on `productbrief2.md` (sections 1–8). Requirement IDs, priorities, measurable acceptance criteria, delivery stages, epics, process conventions and initial test scenarios form the **approved PRD planning baseline**. Approval does not imply that features are implemented, that the course-delivery scope is finalised, or that particular architectures or commercial integrations are available.

---

## 1. Executive Summary

TripWeaver AI enables a traveller to describe a highly personalised travel experience in natural language and receive an organised, realistic itinerary that coordinates activities, accommodation, transportation, weather, costs and bookings across different providers.

Its distinguishing feature is not simply suggesting attractions: **the system should evaluate whether a complex set of activities is feasible together**, explain trade-offs, adapt to changes and help the user complete the necessary reservations. The long-term experience should make many independent travel services feel like one coordinated journey, without hiding where a reservation must still be completed with a provider.

**Product promise (from Product Brief 2):** “Describe exactly what you want to experience, and the AI figures out how to make it happen.”

The course implementation will be defined through a separate delivery scope baseline. The first vertical slice described in Section 13 provides a phased implementation plan, **not a reduction** of the complete TripWeaver AI product vision.

## 2. Problem and Opportunity

Personalised multi-activity travel planning is fragmented. A traveller often needs separate sources for destinations, attractions, opening hours, accommodation, availability, transport routes, weather, prices and bookings. The information must then be reconciled into one schedule.

This is especially difficult when requests combine strict requirements and preferences—for example, a fixed five-day period, a maximum budget, specific experiences, favourable weather for outdoor activities, limited travel time and quieter destinations.

TripWeaver AI should reduce the user's coordination effort by interpreting the request, researching suitable options, checking constraints, presenting feasible alternatives and guiding the user from planning to reservation.

**Core problem statement:** Travellers lack a single, adaptable workflow that turns complex natural-language travel preferences into a realistic, transparent and coordinated itinerary, including clear next steps for booking.

## 3. Product Vision, Goals and Non-Goals

### 3.1 Product goals

| ID | Goal | How to evaluate it (proposed) |
| --- | --- | --- |
| G-01 | Interpret complex natural-language requests | Test prompts are converted into inspectable dates, activities, budget and constraints. |
| G-02 | Create realistic itineraries | Validated test cases identify scheduling conflicts instead of silently ignoring them. |
| G-03 | Optimise across competing constraints | The result explains why activities, times, transport or accommodation were selected. |
| G-04 | Support conversational changes | Editing one activity preserves unaffected schedule items wherever possible. |
| G-05 | Make booking progress transparent | The user can distinguish suggestions, checks, pending steps and provider-confirmed reservations. |
| G-06 | Keep the user in control | Proposed purchases, reservation submissions and consequential changes require explicit user approval. |
| G-07 | Produce a maintainable, testable student project | Requirements can be traced to stories, code changes, test results and documented AI-assisted development decisions. |

### 3.2 Product boundaries

TripWeaver AI does **not** guarantee that every external provider has an accessible booking API, that prices and availability remain unchanged, or that a weather forecast is certain. The system must never present an estimate or recommendation as a verified live fact. It does not make autonomous purchases or change confirmed bookings without the user's approval.

These are integrity requirements for the product—not reasons to remove the coordinated-booking vision from the roadmap.

## 4. Target Users and Jobs to Be Done

*The following user segments are inferred from the use cases in Product Brief 2 and should be validated by the group; the brief does not establish survey-based personas.*

| Segment | Need | Successful outcome |
| --- | --- | --- |
| Independent traveller | Plan a customised holiday without checking many sites | One understandable itinerary reflecting personal preferences. |
| Traveller with a complex activity list | Coordinate several experiences with limited time | A feasible sequence with travel time and constraints considered. |
| Budget-sensitive traveller | Balance experiences, accommodation and transport | Transparent estimated total and lower-cost alternatives. |
| Traveller with specific scheduling or accessibility preferences | Avoid unsuitable timing, routes or activities | Preferences are incorporated, and conflicts are explained. |
| Traveller managing multiple reservations | Know what is booked and what remains | Accurate status per reservation and a consolidated itinerary. |

**Primary job to be done:** “When I describe a trip with many personal requirements, help me find and organise realistic options so I can decide what to do and how to book it without coordinating everything manually.”

## 5. Representative User Scenario

A traveller requests a five-day trip in Italy, with local food, bowling, water-based activities and a mountain hike. The traveller specifies a total budget of €2,000, prefers less crowded areas, and wants outdoor activities scheduled when conditions are favourable.

TripWeaver AI should:

1. Extract destination, duration, preferred activities, budget and scheduling constraints.
2. Distinguish requirements that must be met from preferences that can be traded off.
3. Identify plausible destinations and providers from permitted information sources.
4. Check or flag unknown opening hours, distances, travel time, conditions and reservation requirements.
5. Offer a realistic day-by-day itinerary, estimated costs and explanations.
6. Present alternatives if requested activities cannot all fit.
7. Let the user revise particular parts without discarding the entire plan.
8. Track which elements need booking and which are provider-confirmed.

This scenario is an illustrative acceptance test, **not evidence that any live research or booking integration has been implemented**.

## 6. Main User Journey

| Step | User action | System response | Key failure/edge case |
| --- | --- | --- | --- |
| 1. Describe | Enter a free-text travel request | Parse intent, dates, budget, preferences and activities | Missing destination, dates or conflicting instructions |
| 2. Clarify | Review or answer essential questions | Distinguish hard and soft constraints | Vague or impossible requirements |
| 3. Research | Request recommendations | Find and attribute places, conditions and possible providers | Provider data unavailable, stale or incomplete |
| 4. Plan | Generate a trip | Propose a day-by-day itinerary with locations, buffers and estimated cost | Overlapping times or unrealistic travel gaps |
| 5. Compare | Inspect results | Explain trade-offs and display alternatives where possible | Budget or accessibility constraint cannot be met |
| 6. Revise | Ask for a targeted change | Update affected entries; preserve unrelated entries | Revision affects a pre-existing reservation |
| 7. Reserve | Review booking steps and approve actions | Hand off to providers or submit via authorised integration | Price changes, partial failure or unavailable slot |
| 8. Manage | Return to trip after a change | Identify affected items and propose adjustments | Weather/transport data uncertain or unavailable |

## 7. Prioritisation and Requirement Conventions

All functional requirements have stable IDs so related user stories, implementation commits and test evidence can refer to them.

| Label | Meaning |
| --- | --- |
| **P0 — initial working slice** | High-priority requirement for a coherent end-to-end initial demonstration. Final course-delivery commitments are recorded separately in the scope baseline. |
| **P1 — core product capability** | Part of the full TripWeaver AI product and important for later integrations or a more complete release. |
| **P2 — enhancement** | Valuable, but may follow the foundational features. |

**Requirement status values:** `Proposed`, `Approved`, `In progress`, `Implemented`, `Verified`, `Deferred`. The requirements are **Approved as part of the product specification**. This does not indicate implementation, verification or a final course-delivery commitment. The implementation scope must be recorded separately (Section 13), and a requirement becomes `Verified` only with supporting test evidence.

## 8. Functional Requirements

### 8.1 Natural-language understanding and trip creation (EP-01)

| ID | Priority | Requirement | Acceptance criteria (observable outcome) | Brief reference |
| --- | --- | --- | --- | --- |
| FR-001 | P0 | Accept a free-text travel description | A user can submit a request containing destination, dates or duration, budget and activities without completing separate forms first. | §1–3 |
| FR-002 | P0 | Extract and display trip parameters | The system returns structured values for identifiable dates, places, activities, budget and preferences; it flags missing or ambiguous values. | §2–3 |
| FR-003 | P0 | Separate hard constraints and soft preferences | A fixed budget/date is not silently relaxed; a preference such as quieter locations is labelled as flexible. | §3, §5 |
| FR-004 | P0 | Clarify material ambiguities | The system asks for a necessary missing input rather than inventing it; optional ambiguities can be stated as assumptions. | §3 |
| FR-005 | P1 | Retain preferences within a trip | Follow-up requests use the current trip constraints unless the user explicitly changes them. | §3 |
| FR-006 | P2 | Support multiple languages and currencies | Supported languages/currencies can be selected and displayed consistently; conversions identify their assumptions. | §3 |

### 8.2 Research and source reliability (EP-02)

| ID | Priority | Requirement | Acceptance criteria (observable outcome) | Brief reference |
| --- | --- | --- | --- | --- |
| FR-007 | P0 | Present research-backed or explicitly unverified options | Places and activities display what is known, estimated and unknown; factual assertions are not presented as verified without a source. | §4 |
| FR-008 | P1 | Retrieve destination/provider details from permitted sources | Where integrations exist, suggestions can include address, hours, prices, restrictions and links; missing fields remain marked unknown. | §4 |
| FR-009 | P1 | Check current availability through an authorised provider source | Availability is shown as verified only when supported by a current response; the provider and time checked are recorded. | §4, §6 |
| FR-010 | P1 | Combine maps, route and travel-time information | Planned transitions include a sourced or clearly estimated travel duration; infeasible transitions trigger a warning. | §4–5 |
| FR-011 | P1 | Consider weather and seasonal conditions | Outdoor suggestions consider available forecast and relevant restrictions; uncertainty and forecast age are communicated. | §4–5 |

### 8.3 Scheduling, feasibility and optimisation (EP-03)

| ID | Priority | Requirement | Acceptance criteria (observable outcome) | Brief reference |
| --- | --- | --- | --- | --- |
| FR-012 | P0 | Generate a structured daily itinerary | Each day includes ordered itinerary items with an activity, planned time or duration and a location or explanation when unknown. | §2, §5 |
| FR-013 | P0 | Detect obvious itinerary conflicts | Overlaps, impossible sequences and violations of explicit fixed times are reported instead of silently accepted. | §5 |
| FR-014 | P0 | Explain infeasibility and propose adjustments | For an impossible test request, the user receives a reason and one or more reasonable changes, not a fabricated feasible plan. | §2, §5 |
| FR-015 | P1 | Optimise for travel, opening hours, buffers and preferences | Where required data exists, the itinerary incorporates opening hours, preparation and travel buffers, daylight and soft constraints; trade-offs are explained. | §5 |
| FR-016 | P1 | Generate alternative itineraries | The user can compare feasible options by cost, travel or preference match, where sufficient data exists. | §3, §5 |

### 8.4 Editing and dynamic management (EP-04)

| ID | Priority | Requirement | Acceptance criteria (observable outcome) | Brief reference |
| --- | --- | --- | --- | --- |
| FR-017 | P0 | Support conversational itinerary revisions | The user can request “move the activity” or “choose a cheaper option”; the result shows which items changed. | §3, §7 |
| FR-018 | P0 | Preserve unaffected itinerary items | A targeted revision leaves unrelated items unchanged unless a dependency requires an adjustment, which is explained. | §3, §7 |
| FR-019 | P1 | Suggest changes after verified disruptions | When supported data indicates a closure or forecast change, the system proposes a new plan and identifies impacted reservations. | §7 |
| FR-020 | P1 | Save and restore planned trips | A user can return to a stored itinerary and see the same confirmed changes and booking states, subject to agreed account design. | §7 (inferred supporting capability) |

### 8.5 Accommodation and budget (EP-05)

| ID | Priority | Requirement | Acceptance criteria (observable outcome) | Brief reference |
| --- | --- | --- | --- | --- |
| FR-021 | P0 | Display an estimated trip budget | The plan shows an estimated total by relevant categories and identifies missing costs, currencies and assumptions. | §2, §5 |
| FR-022 | P1 | Recommend accommodation using trip context | Options consider activity proximity, transport, price, amenities and stated preferences; unknown availability is disclosed. | §8 |
| FR-023 | P1 | Recalculate estimates after changes | When activities, transport or accommodation change, affected estimates are recalculated or identified as unavailable. | §2, §3, §8 |

### 8.6 Coordinated booking and reservation state (EP-06)

| ID | Priority | Requirement | Acceptance criteria (observable outcome) | Brief reference |
| --- | --- | --- | --- | --- |
| FR-024 | P0 | Show booking requirements and provider handoffs | The itinerary identifies which items require reservation and offers a provider handoff where a genuine destination is available. | §6 |
| FR-025 | P1 | Present a consolidated reservation summary | The user sees provider, item, displayed price/source, conditions and current booking status per item. | §6 |
| FR-026 | P1 | Submit bookings only through supported, authorised integrations | A submission is attempted only where permitted integration exists and after explicit user approval of the relevant details and charges. | §6 |
| FR-027 | P1 | Track verifiable booking outcomes | An item is marked `Confirmed` only with provider confirmation; failed and pending bookings remain separately identified. | §6 |
| FR-028 | P1 | Recover from partial booking failures | A failed booking does not silently affect unrelated confirmations; the user is told which components succeeded, failed or need manual action. | §6 |
| FR-029 | P1 | Require consent before changes to reservations | Cancellation, payment or rebooking is never automatically executed without clear approval and an explanation of relevant costs. | §6–7 |

### 8.7 User experience and information presentation (EP-07)

| ID | Priority | Requirement | Acceptance criteria (observable outcome) | Brief reference |
| --- | --- | --- | --- | --- |
| FR-030 | P0 | Show a readable trip overview | Days, activities, estimates, assumptions and booking steps are discoverable without interpreting raw AI output. | §1–2, §6 |
| FR-031 | P0 | Give clear feedback on errors and uncertainty | Invalid input, missing sources and failed AI/API requests produce actionable messages instead of a crash or fabricated result. | §4–6 |
| FR-032 | P1 | Provide map-oriented itinerary review | When geographic data is available, locations and activity order can be inspected on a map or equivalent route view. | §4–5 |

### 8.8 Business rules and invariants

These rules apply regardless of integration vendor or phase:

- **BR-01 — Constraint integrity:** The system may propose relaxing a hard constraint but must not silently relax it.
- **BR-02 — No invented availability:** A place appearing in search or on a map is not evidence of bookability.
- **BR-03 — Source honesty:** Verified facts, forecasts, estimates and AI-generated suggestions must be distinguishable.
- **BR-04 — Explicit booking approval:** All purchase/reservation submissions require informed user approval.
- **BR-05 — Confirmations come from providers:** Only provider-confirmed bookings can be labelled `Confirmed`.
- **BR-06 — Localised updates:** A revision must preserve unaffected itinerary elements where practical and expose necessary dependent changes.
- **BR-07 — Uncertain conditions:** Weather, schedules and prices are presented with relevant uncertainty and source age where applicable.
- **BR-08 — Provider restrictions:** The application must identify relevant participation, accessibility and safety limitations where known, and avoid claiming that an activity is suitable without adequate information.

## 9. AI Behaviour and Decision Logic

The LLM interprets requests and proposes itinerary choices. It must not be treated as an authoritative source of real-time prices, availability, opening hours or provider confirmations.

**Proposed reasoning-to-output contract (technology-neutral):**

1. **Parse:** Extract structured fields and the user's original wording.
2. **Classify:** Record each requirement as `hard`, `soft`, or `needs clarification`.
3. **Ground:** Attach known locations, providers, data timestamps and permitted sources.
4. **Validate:** Check for scheduling, distance, opening-hour and budget conflicts using available data.
5. **Optimise:** Prefer feasible schedules and explain any competing priorities.
6. **Explain:** Mark assumptions and unresolved dependencies.
7. **Revise:** Update only dependent schedule elements when possible.
8. **Confirm:** Keep provider booking actions separate from generated advice and require human approval.

**Suggested structured output fields:** `trip_id`, `destination`, `date_range`, `travellers`, `currency`, `constraints[]`, `days[]`, `items[]`, `cost_estimates[]`, `source_references[]`, `warnings[]`, `booking_actions[]`, `verification_status`.

This is an **illustrative data contract**, not an agreed technical architecture. The architecture document should define types, persistence and validation after the team selects a stack.

## 10. Reservation State Model

| State | Meaning | May the UI say “booked”? |
| --- | --- | --- |
| `Suggested` | AI or research result, possibly unverified | **No** |
| `Availability checked` | Source returned availability at a recorded time | **No** |
| `Action required` | User must book externally or approve an action | **No** |
| `Pending` | A booking attempt is in progress or awaiting verification | **No** |
| `Confirmed` | Provider has returned a confirmation | **Yes** |
| `Failed / unavailable` | Attempt failed or slot cannot be verified | **No** |

Each reservation should retain the provider, source URL or integration reference, last verification time and confirmation identifier **only when returned by the provider**. Do not fabricate confirmations in demonstrations; simulated examples must be conspicuously labelled as simulations.

## 11. Non-Functional Requirements

| ID | Category | Requirement and verification approach |
| --- | --- | --- |
| NFR-001 | Usability | Primary flow (request → itinerary → review/revise) is navigable with readable status messages. Verify through moderated walkthroughs. |
| NFR-002 | Responsive design | Main screens remain usable at common mobile and desktop widths; check at representative sizes selected by the team. |
| NFR-003 | Accessibility | Support meaningful labels, keyboard access, visible focus, text alternatives and readable contrast. Verify with a manual accessibility checklist. |
| NFR-004 | Reliability | Invalid requests, provider outages and repeated submissions do not crash the application or incorrectly create confirmations. Test intentional failure cases. |
| NFR-005 | Transparency | Any displayed availability, price or condition indicates whether it is verified, estimated or unknown; record source/time where used. |
| NFR-006 | Data protection | Limit personal data, restrict access to saved trips and define data retention/deletion rules appropriate to the implementation. |
| NFR-007 | Secrets and configuration | Keep API keys and credentials out of source control and client-side bundles; supply example environment variables without secrets. |
| NFR-008 | Maintainability | Use readable modules, documented dependencies, input validation and an architecture consistent with the implementation. |
| NFR-009 | Observability | Capture useful development/test error information without logging sensitive credentials, full payment details or unnecessary personal information. |
| NFR-010 | Reproducibility | A new reviewer can install, configure, run and test the app using the versioned README instructions. |
| NFR-011 | External-service compliance | Use official/licensed APIs or otherwise permitted access within provider limitations. |
| NFR-012 | Performance | Display loading/progress and provide recovery from delays; **numeric performance thresholds require a baseline and team approval**. |

The sensor guide requires evidence of functioning tests, usability, maintainable architecture and README-driven reproducibility; the specific NFR IDs and test methods above are proposed translations for this project.

## 12. Dependencies, Risks and Assumptions

| ID | Dependency / risk | Impact | Planned mitigation / decision needed |
| --- | --- | --- | --- |
| R-01 | Booking APIs are not available to a student project | Full booking workflow may not be implemented initially | Use authenticated partner APIs if available; otherwise a transparent provider handoff; do not imply a confirmed booking. |
| R-02 | LLM hallucination of venues, times or prices | Misleading or infeasible plans | Cross-check with permitted sources; validate constraints; label assumptions. |
| R-03 | Weather and availability change | A plan becomes outdated | Store source timestamps, offer refresh and user-approved revision. |
| R-04 | Too many coupled features for the course timeframe | Unfinished core flow | Agree a baseline vertical slice, then integrate progressively; log scope changes. |
| R-05 | Multi-provider transaction partially succeeds | User confusion or costs | Represent each reservation separately and show precise state. |
| R-06 | Personal travel data or credentials leak | Trust and security failure | Data minimisation, access controls, secure configuration and no committed secrets. |
| R-07 | API rate limits, costs and licensing | Interrupted demonstration | Check terms and budgets; provide clear error/fallback behaviour or labelled demo fixtures. |
| R-08 | PRD and delivered app diverge | Sensor cannot trace what was promised | Update PRD/decision log alongside changes; map stories, commits and tests to requirements. |
| R-09 | Approved course proposal may set different commitments | Wrong delivery baseline | **Check the approved proposal against this PRD before approving scope.** |

**Unverified assumptions:** The team has not yet documented the selected LLM, map service, weather service, database, payment/booking partners, hosting approach or approved delivery scope in this PRD. Do not treat any particular provider as already integrated or any requirement as complete.

## 13. Release Plan and Milestones

**This phased development sequence is part of the approved PRD.** It provides an implementation roadmap; the scope committed for the course submission must still be confirmed. The full vision in Product Brief 2 remains the product target.

| Stage | Outcome | Requirements to target | Exit evidence |
| --- | --- | --- | --- |
| **A. Initial end-to-end slice** | Free-text request becomes a structured and editable travel itinerary with estimates, source/uncertainty labels and booking checklist. | FR-001–004, FR-007, FR-012–014, FR-017–018, FR-021, FR-024, FR-030–031 | Working demo, user scenario tests, commits, QA evidence. |
| **B. Context-aware planning** | Add real-place research, travel durations, weather, accommodation evaluation and saving trips. | FR-005, FR-008, FR-010–011, FR-015, FR-020, FR-022–023, FR-032 | Integration tests, source/error-handling evidence, updated README. |
| **C. Coordinated booking** | Integrate live availability and authorised bookings, or clearly documented provider handoffs where integrations are not possible. | FR-009, FR-025–029 | Provider responses or labelled test fixtures, approval flow and booking-state tests. |
| **D. Expanded optimisation** | Multiple itinerary comparisons, dynamic re-planning and broader language/currency options. | FR-006, FR-016, FR-019 | Comparative and disruption test scenarios. |

**Scope baseline required:** Before implementation, mark each requirement as `Committed for course submission`, `Conditional on integration`, or `Post-course roadmap`. Record the decision in Section 20 and maintain traceability. If the approved proposal already commits to particular features, the group must honour them or formally document a justified change.

### Scope decision table (to complete at implementation planning)

| Item | Proposed baseline | Final group decision |
| --- | --- | --- |
| Natural-language itinerary creation | Commit | **Pending** |
| Constraint handling and revisions | Commit | **Pending** |
| At least one real-data integration | Evaluate feasibility | **Pending** |
| Persisted trips and user accounts | Decide based on architecture and proposal | **Pending** |
| Direct provider booking | Conditional on authorised integration | **Pending** |
| Booking handoff and honest statuses | Commit | **Pending** |
| Mobile-responsive interface | Commit | **Pending** |
| Technology stack, deployment and test tools | Decide in architecture | **Pending** |

## 14. Candidate Epics and User Stories (BMAD Handoff)

These epics are **planning candidates**. They are not claims that GitHub issues, implementation branches or story documents already exist.

| Epic | Scope | Linked requirements |
| --- | --- | --- |
| EP-01 | Request intake, parameter extraction and clarification | FR-001–006 |
| EP-02 | Research, sources, maps and environmental conditions | FR-007–011 |
| EP-03 | Feasible scheduling and optimisation | FR-012–016 |
| EP-04 | Conversational editing and trip management | FR-017–020 |
| EP-05 | Accommodation and cost optimisation | FR-021–023 |
| EP-06 | Coordinated booking and booking status | FR-024–029 |
| EP-07 | Trip overview, errors, UX and accessibility | FR-030–032, NFR-001–003 |
| EP-08 | Technical quality, security, tests and operations | NFR-004–012 |

### Example story US-001 — Create a trip from natural language

**As a** traveller, **I want** to describe my trip in ordinary language, **so that** I can begin planning without filling out numerous forms.

- **Linked requirements:** FR-001, FR-002, FR-004.
- **Given** a valid free-text travel request containing dates, budget and activities, **when** I submit it, **then** the system shows an interpreted trip with those details.
- **Given** an essential detail cannot be inferred, **when** the request is parsed, **then** the application asks for clarification or highlights the missing field.
- **Definition of done:** UI implemented, parsing tests recorded, failure path tested, review performed and README/demo instructions updated where necessary.

### Example story US-002 — Resolve a hard scheduling conflict

**As a** traveller, **I want** impossible schedules to be flagged, **so that** I do not rely on a plan that cannot work.

- **Linked requirements:** FR-003, FR-013, FR-014.
- **Given** two fixed activities whose times overlap, **when** the itinerary is generated, **then** a conflict is reported and an adjustment is suggested without silently changing the fixed constraint.
- **Definition of done:** at least one successful and one conflicting case tested, including the validation result and a reviewer note.

### Example story US-003 — Review reservation status

**As a** traveller, **I want** to know which experiences actually have reservations, **so that** I do not mistake a suggested provider for a confirmed booking.

- **Linked requirements:** FR-024, FR-025, FR-027, BR-05.
- **Given** a proposed activity with no provider confirmation, **when** I view my itinerary, **then** it is not labelled `Confirmed`.
- **Given** a genuine provider confirmation is recorded, **when** I view the same activity, **then** its status changes to `Confirmed` with its provider reference.
- **Definition of done:** state mapping and tests documented; simulation/fixture data explicitly labelled.

**Story handoff template:** Every future story should include `Story ID`, `User value`, `Linked FR/NFR/BR IDs`, `Acceptance scenarios`, `Dependencies`, `Implementation PR/commits`, `Tests`, `Review/AI decisions`, and `Status`.

## 15. Verification and Test Plan

A student project should not claim a requirement is complete merely because a generated UI looks convincing. Tests must verify real logic, error paths and quality review.

| Test ID | Scenario | Linked requirements | Expected result | Suggested test type |
| --- | --- | --- | --- | --- |
| T-001 | Parse a five-day itinerary request | FR-001–002 | Correctly structured dates/duration, budget and activities | Unit/integration |
| T-002 | Omit a vital field | FR-004, FR-031 | Clear clarification request or explicit unresolved status | Unit/UI |
| T-003 | Fixed time overlap | FR-003, FR-013–014 | Conflict shown; fixed requirement not silently altered | Unit/integration |
| T-004 | Impossible travel gap | FR-010, FR-013–015 | Route gap warned or an alternative proposed | Integration |
| T-005 | Targeted conversational revision | FR-017–018 | Requested item changes; unrelated items preserved when feasible | Integration/end-to-end |
| T-006 | Lower total budget | FR-021, FR-023 | Adjusted estimates/trade-offs; unknown prices disclosed | Integration |
| T-007 | Weather-dependent activity | FR-011, FR-019 | Forecast uncertainty displayed; change suggested rather than guaranteed | Integration with fixture |
| T-008 | Provider unavailable or API failure | FR-007–009, FR-031 | No fabricated venue details or confirmed status; actionable feedback | Failure injection |
| T-009 | Booking without confirmation | FR-024–028, BR-05 | Status stays non-confirmed | Unit/integration |
| T-010 | Booking approval gate | FR-026, FR-029 | No submission/rebooking without explicit approval | Integration |
| T-011 | Repeated actions / invalid data | FR-031, NFR-004 | No crash, duplicate booking or corrupted state | Unit/end-to-end |
| T-012 | Mobile and keyboard usage | FR-030, NFR-001–003 | Main flow usable with keyboard and on selected mobile width | Manual UX/accessibility |
| T-013 | Clean environment setup | NFR-007–010 | Reviewer can install/run/test via README only | Clean-machine smoke test |
| T-014 | Code review of AI-generated change | NFR-008–009 | Review identifies validation/security concerns and records corrections | Peer review evidence |

**Testing evidence to retain:** command or procedure, date, environment, input, expected result, observed result, pass/fail, related requirement, commit/PR, and (when relevant) screenshots or logs with secrets removed. Do not mark a planned test as passing until it has actually run.

### Exit criteria for a course submission (proposed)

- Every **committed** requirement is either `Verified` or has a documented deviation explaining impact and next steps.
- The primary user journey works from start to finish without invented live results.
- Critical failure cases have been demonstrated and recorded.
- Relevant automated tests are runnable as documented in the README; manual tests are documented where automation is unsuitable.
- At least one documented example shows the team reviewing and correcting an AI-generated suggestion or implementation.
- A clean reviewer can start the application using only the README and example configuration.

## 16. User Experience and Interface Expectations

**Key screens or sections (proposed):**

1. **Travel request:** Natural-language input with examples and an explicit submit action.
2. **Requirements review:** Extracted parameters, hard/soft constraints and unresolved questions.
3. **Trip overview:** Day-by-day activity sequence, travel gaps, costs and identified assumptions.
4. **Options detail:** Provider/location details, data provenance, times and restrictions.
5. **Revision flow:** A conversational edit with visible change summary.
6. **Booking centre:** Reservation checklist, handoff links, approvals and accurate statuses.

The team should produce simple wireframes or a UI description and document navigation, empty states, error states, accessibility decisions and mobile behaviour. **No wireframe is claimed to exist yet.**

## 17. Architecture and Data Handoff (Not Yet Decided)

The architecture document should specify the chosen language/framework, repository structure, database, third-party APIs, secure key handling, application states, test framework and deployment method. It should explain how requests flow from the interface through parsing, research, scheduling, persistence and reservation status.

**Suggested conceptual data objects:** `Trip`, `TripConstraint`, `UserPreference`, `TripDay`, `Activity`, `Place`, `SourceEvidence`, `CostEstimate`, `ReservationAction`, `BookingState`, `ProviderConfirmation`.

**Important design rules:**

- Keep estimated information separate from provider-verified information.
- Ensure hard constraints are validated independently of free-form LLM text where feasible.
- Use structured state transitions for reservations and prevent a generated response from fabricating `Confirmed`.
- Keep API credentials on the server or other appropriately protected environment.
- Clearly identify any mocked/test data in a demo.

The data objects and architecture suggestions are illustrative, not binding technology choices.

## 18. Traceability: From Plan to Evidence

The sensor guide places particular emphasis on a traceable path from plan to code, plus commits, prompts, iterations and decisions. For each implemented requirement, maintain a record like the one below.

| Requirement | Epic / story | Code / PR | Test evidence | Decision / change | Status |
| --- | --- | --- | --- | --- | --- |
| FR-001 | EP-01 / US-001 | _Add when implemented_ | T-001 | _Add if changed_ | Proposed |
| FR-013 | EP-03 / US-002 | _Add when implemented_ | T-003 | _Add if changed_ | Proposed |
| FR-017 | EP-04 / _Story to create_ | _Add when implemented_ | T-005 | _Add if changed_ | Proposed |
| FR-024 | EP-06 / US-003 | _Add when implemented_ | T-009 | _Add if changed_ | Proposed |
| NFR-010 | EP-08 / _Story to create_ | _Add when implemented_ | T-013 | _Add if changed_ | Proposed |

**Proposed evidence conventions (paths are examples to be created, not existing files):**

| Artifact | Suggested location | Purpose |
| --- | --- | --- |
| Product brief | `productbrief2.md` | Original full product vision |
| PRD | `docs/planning/prd.md` | Approved and updated requirements |
| Architecture | `docs/planning/architecture.md` | Technology decisions and structure |
| Epics/stories | `docs/planning/epics/` | Small, testable work items |
| AI prompt/iteration log | `docs/process/ai-log.md` | Prompt, response, evaluation, correction and resulting change |
| Decision log | `docs/process/decisions.md` | Rationale for trade-offs and scope changes |
| Test report/evidence | `docs/testing/` | Tests run, observed results and fixes |
| README | `README.md` | Reproducible install/run/test instructions and documentation map |

**Example AI decision record:** `Date → Requirement ID → Original prompt/task → AI suggestion → Our evaluation → Accepted/rejected/modified → Reason → Code/PR → Test outcome`. Save actual evidence; do not invent previous prompts or decisions for the portfolio.

## 19. Development Process and Quality Controls

This section translates the IBE160 marking guide into an **intended workflow**, not a claim of completed work.

1. **Plan:** Agree on PRD scope and create an architecture document plus prioritised stories.
2. **Implement in small steps:** Use focused branches/commits or equivalent group workflow; reference the story/requirement ID.
3. **Use AI deliberately:** Record representative prompts and resulting changes, especially where the team challenged, corrected or rejected an AI suggestion.
4. **Review:** Check generated code for correctness, readability, security, duplicated code and handling of external data.
5. **Test:** Run meaningful automated tests for critical logic and record manual UX checks where appropriate.
6. **Update documentation:** Amend requirements, stories and decisions when implementation changes; keep README aligned with the app.
7. **Demonstrate:** Repeat the clean-environment install and the primary user scenarios before submission.

**Assessment relevance:** The provided sensor guide allocates 30% of *Part 1* to process and AI management, 20% to functionality, 15% to testing, 10% each to UX, architecture and README, and 5% to repository hygiene. These are **weights within Part 1** (which contributes 70% of the overall grade), not weights for the PRD itself. The guide explicitly names product briefs, PRDs, architecture, epics and stories as examples of BMAD planning evidence and warns against documents generated once but never used.

## 20. Open Decisions and Change Control

### 20.1 Open implementation decisions (next planning meeting: 5 November 2026)

| ID | Decision needed | Why it matters | Status |
| --- | --- | --- | --- |
| D-01 | Confirm PRD alignment with the approved proposal | Sensor compares delivery against promised functionality | Open |
| D-02 | Agree the committed first release scope | Prevent ambiguity between product vision and submission | Open |
| D-03 | Select backend/frontend architecture and persistence | Allows implementable stories and tests | Open |
| D-04 | Choose LLM, geocoding/maps and weather sources | Determines feasibility, cost and terms | Open |
| D-05 | Decide direct booking vs provider handoff for the course submission | Affects central product differentiator and integration tests | Open |
| D-06 | Decide whether accounts and saved trips are in the first release | Affects privacy, authorization and architecture | Open |
| D-07 | Agree who approves PRD changes and where evidence is recorded | Supports traceability across group members | Open |
| D-08 | Select measurable usability/performance targets after an initial baseline | Makes success criteria fair and testable | Open |

### 20.2 Document change log

| Version | Date | Change | Approval |
| --- | --- | --- | --- |
| 0.1 | 4 Nov 2026 | Initial proposed PRD draft | Not recorded |
| 0.2 | 4 Nov 2026 | Align to `productbrief2.md` and IBE160 assessment guide; add stable requirement IDs, acceptance tests, BMAD handoff, traceability, status rules and decisions | Submitted for review |
| **1.0** | **4 Nov 2026** | Finalise the approved PRD; record approval while preserving open delivery-scope, architecture and integration decisions | **Approved** |

**Change policy:** When a significant requirement changes, update its PRD entry, story, linked tests and decision rationale in the same development cycle. Do not rewrite history to make the original plan look more accurate after the fact.

## 21. Definition of Ready / Definition of Done

### Definition of Ready for a story

- Clear user value and linked FR/NFR/BR identifiers.
- Observable acceptance criteria and failure cases.
- Known dependencies and suitable test approach.
- Decision made on any scope or data-source ambiguity that blocks implementation.

### Definition of Done for an implemented story

- Acceptance criteria met in the running application (not just generated text or mocks).
- Tests performed and results recorded; failures resolved or documented.
- AI-generated code has been reviewed by a team member.
- Security and privacy implications reviewed for the changed functionality.
- Related PRD, architecture, story and README sections updated if relevant.
- Commit/PR references and any significant AI decisions linked to the requirement.

## 22. Source and Interpretation Notes

1. **Primary product source:** [`productbrief2.md`](https://github.com/IBE160-2026/G103-berge-hagen-holmen-nguyen/blob/main/productbrief2.md), sections 1–8. It establishes TripWeaver AI as an ambitious natural-language, research, scheduling and coordinated-booking product. This PRD preserves those capabilities as the full product target.
2. **Course assessment source:** *Sensorveiledning IBE160 – Del 1, applikasjon og prosess*, autumn 2026. Particularly relevant are page 2 (planned BMAD documents and plan-to-code traceability), page 3 (delivery relative to proposal, testing criteria), page 4 (UX and evidence), page 5 (architecture and README), and pages 6–7 (repository quality and red flags).
3. **Open implementation dependencies:** Alignment with the group's approved proposal, any course-specific PRD template, selected technical architecture, actual commits, the course-delivery scope and real test outcomes has not yet been verified within this document. Approval of this PRD does not establish that these decisions or deliverables exist; they must be documented as the project develops.

---

**End of PRD v1.0 — Approved planning baseline.**